# video-shot-agent

레퍼런스 영상을 씬 단위로 분석한 뒤, 각 샷을 Higgsfield로 재생성하는 에이전트 스킬.

## 트리거 조건

다음 중 하나에 해당하면 이 스킬을 로드한다:
- `/video-shot-agent` 슬래시 명령
- "레퍼런스 영상으로 샷 생성", "영상 분석 후 재생성", "shot agent" 등의 요청
- YouTube 링크 또는 업로드 영상과 함께 샷 재생성 요청

## 실행 단계

### 1. 입력 수집

| 입력 | 방법 |
|------|------|
| YouTube URL | 그대로 사용 |
| 로컬/첨부 파일 | `mcp__Higgsfield__media_upload_widget` 를 단독 호출 |
| 웹 URL (비YouTube) | `mcp__Higgsfield__media_import_url` |

> **규칙**: media_id 없이 로컬/첨부 파일이 들어오면 `media_upload_widget`을 그 턴의 유일한 도구 호출로 실행한다. `/mnt/user-data/uploads` 직접 접근 금지.

### 2. 영상 분석 (video_analysis_create)

```
mcp__Higgsfield__video_analysis_create
  youtube_url: <URL>          # YouTube인 경우
  OR
  video_input_id: <media_id>  # 업로드 영상인 경우
```

- 반환값 `video_analyze_id` 를 보관한다.
- 사용자에게: "분석을 시작했습니다. 보통 3~5분 소요됩니다."
- **영상이 길수록 씬 분석 정확도가 낮아진다. 짧은 클립이 최적.**

### 3. 분석 완료 대기 (video_analysis_status 폴링)

```
mcp__Higgsfield__video_analysis_status
  video_analyze_id: <id>
```

- 30~60초 간격으로 폴링. `status == 'completed'` 될 때까지 반복.
- `status == 'failed'` 이면 `fail_reason` 을 사용자에게 전달하고 종료.

### 4. 씬 목록 파싱 및 프롬프트 설계

완료된 분석 결과의 `scenes` 배열에서 각 씬을 추출한다.

각 씬마다:
- `scene_description` (또는 동등 필드)를 기반으로 **영어 생성 프롬프트** 작성
- 원본 씬의 분위기·카메라 무브·색감을 반영한다
- 프롬프트 구성 8요소를 최대한 포함한다:
  - **이미지 5요소**: Subject, Background, Composition, Lighting, Style
  - **영상 추가 3요소**: Camera Move, Subject Motion, Cut Duration
  - **오디오 3요소** (audio 있을 경우): BGM, SFX, Dialogue
- 기본 모델 선택 기준:

| 용도 | 추천 모델 | 비고 |
|------|-----------|------|
| 최고 품질 영상 | `seedance_2_5` | 크레딧 높음, end-game |
| I2V·모션 컨트롤 | `kling3_0` | 가성비·품질 균형 최고 |
| 빠른 드래프트 | `grok_imagine_2` | 속도·비용 우선 |
| 일상·가성비 | `minimax_h3` | 멀티샷 지원 |
| 4K 이미지 | `nano_banana_pro` or `gpt_image_2` | 텍스트 있으면 GPT |
| **비추천** | `wan_2_7` | 모션 부자연스러움 |

### 5. 샷 생성 (generate_video_batch)

씬이 2개 이상이면 `generate_video_batch` 로 병렬 처리한다.
씬이 1개이면 `generate_video` 를 사용한다.

```
mcp__Higgsfield__generate_video_batch
  jobs:
    - model: seedance_2_5
      prompt: <씬1 프롬프트>
      aspect_ratio: <원본과 동일>
    - model: seedance_2_5
      prompt: <씬2 프롬프트>
      ...
```

> `generate_video_batch` 한 번에 최대 12개. 12개 초과 시 그룹으로 나눈다.

### 6. 완료 대기 (jobs_wait)

```
mcp__Higgsfield__jobs_wait
  jobs:
    - index: 0
      job_id: <job_id_0>
    - index: 1
      job_id: <job_id_1>
    ...
  timeout_seconds: 15
```

`all_terminal == false` 이면 `poll_after_seconds` 후 재호출한다.

### 7. 결과 표시 (show_generation_by_ids)

모든 job이 terminal 상태가 되면:

```
mcp__Higgsfield__show_generation_by_ids
  job_ids: [<job_id_0>, <job_id_1>, ...]
```

---

## 도구 목록 (allowed-tools)

이 스킬이 사용하는 Higgsfield 도구:

- `mcp__Higgsfield__media_upload_widget`
- `mcp__Higgsfield__media_import_url`
- `mcp__Higgsfield__video_analysis_create`
- `mcp__Higgsfield__video_analysis_status`
- `mcp__Higgsfield__generate_video`
- `mcp__Higgsfield__generate_video_batch`
- `mcp__Higgsfield__jobs_wait`
- `mcp__Higgsfield__show_generation_by_ids`

## 제약 및 규칙

- 크레딧 소모 전 사용자에게 씬 목록과 예상 생성 수를 보여주고 확인을 받는다.
- `use_unlim` 은 사용자가 명시적으로 요청할 때만 `true` 로 설정한다.
- 분석 결과가 0개 씬이면 "분석 결과가 없습니다"를 전달하고 종료한다.
- 12개 초과 씬은 그룹 처리하며 진행 상황을 사용자에게 알린다.
- `generate_video`/`generate_video_batch` 의 `medias[].value` 에는 반드시 media_id/job_id만 전달한다 (https:// URL 금지).

## Tier 정의

| Tier | 동작 |
|------|------|
| Tier 1 | 분석만 수행, 씬 목록 출력 (생성 없음) |
| Tier 2 | 씬 1개만 선택해 end-to-end 생성 검증 |
| Tier 3 | 전체 씬 생성 |

기본값: **Tier 2** (레퍼런스 영상 1개로 검증 후 Tier 3 진행)

---

## 핵심 학습 (Higgsfield MCP 튜토리얼 영상 기반)

### 3단계 프로덕션 원칙

```
Text(기획) → Image(검토) → Video(완성)
```
- 영상 바로 생성 금지. 이미지로 먼저 확인 후 진행.
- Claude 기획 단계는 크레딧 소모 없음. 영상 5초 ≈ 50 크레딧.

### MCP 권한 설정 권장값

| 도구 | 설정 |
|------|------|
| Cancel Auto-renewal | Block |
| Generate 3D / Audio / Image / Video | Ask Permission |
| Upload Media / Sync Agents | Always Allow |

### 캐릭터 일관성: @me 등록

1. 셀카 6장 (정면·측면·위아래)
2. GPT Image 2.0으로 4K 캐릭터 시트 생성
3. Cinema Studio → My Elements → `@me` 등록
4. Claude 프롬프트: `"Me가 주인공, Office가 배경"`

### 유용한 내장 앱

| 앱 | 용도 |
|----|------|
| Bullet Time Scene | 사진 1장 → 제품 360° 회전 영상 |
| Mixed Media → Canvas | 실제 영상 → 애니메이션 스타일 변환 |

### Claude 붙여넣기 팁

- 긴 텍스트: `Ctrl+Shift+V` (서식 없이 붙여넣기)

### 프롬프트 국가·모델 지정 (필수)

- 기본값은 **서양 모델·배경** 출력 → 한국 콘텐츠는 반드시 명시
- 예: `Korean female model in her 20s, Korean indoor background`
- Seedance 2.0은 **4K** 버전 별도 존재 → 최종 출력 시 `Seedance 2.0 4K` 지정

### 광고 영상 배치 생산 패턴

5가지 유형 콘텐츠 플랜 → 배치 생성:
`Review → Unboxing → Street Interview → Challenge → ASMR`

### Seedance 2.5 vs 2.0 품질 차이

| 항목 | 2.0 | 2.5 (`seedance_2_5`) |
|------|-----|-----|
| 해상도 엔진 | 720p 수준 | 1080p 선명 |
| 패브릭 물리 | 뭉개짐 | 자연스러운 주름·움직임 |
| 배경 왜곡 | 발생 | 없음 |
| 색감 | 보통 | 더 선명한 채도·대비 |

- **모션 컨트롤 슬라이더**: Speed + Intensity로 세밀 조정 가능
- 항상 `seedance_2_5` 사용 — 2.0은 구버전

### 쇼츠 광고 5씬 구조 (35초 숏폼)

```
Hook (0~5s) → 비교/증거 (5~13s) → 기능 설명 (13~21s)
→ 활용 사례 몽타주 (21~29s) → CTA (29~35s)
```

### 크레딧 비용 (Seedance 기준)

| 해상도 | 길이 | 크레딧 |
|--------|------|--------|
| 1080p | 8초 | 72 |
| 4K | 8초 | 176 |

- 드래프트는 1080p, 최종만 4K 재생성

### 얼굴·캐릭터 일관성 프롬프트 (필수)

- 모든 영상 프롬프트에 `"keep the same character"` 포함
- 없으면 씬마다 얼굴이 달라질 수 있음
- 가상 한국인 모델: `"original fictional Korean woman"` 명시

### 로고 보존 (제품 광고)

- 제품 이미지 + 로고 파일 동시 업로드
- 프롬프트: `"do NOT redraw or change the logo, preserve logo exactly"`
- 제품은 고정, 배경(빛·파티클·안개)만 움직이게 설계 → 로고 왜곡 방지

### 긴 영상 제작 전략

- 8~15초 클립 단위 생성 → 외부 편집 툴에서 이어붙이기
- Higgsfield 내 단일 긴 영상보다 클립 조합이 품질 우수

### 주의: 모바일 앱 비공식

- App Store / Google Play의 Higgsfield 앱은 **비공식** → 웹 버전만 사용
