# Higgsfield 학습 내용 (영상 분석 기반)

## 영상 5: Higgsfield A-Z 실전 워크플로우 (내 얼굴로 광고 만들기)
URL: https://youtu.be/Nc6ywbkTmZU
씬 수: 79개

### 전체 A-Z 워크플로우 (사진 → 이미지 → 영상)

```
1. 내 사진 업로드 (media_upload_widget)
2. GPT Image 2.0으로 캐릭터 이미지 생성 (내 얼굴 레퍼런스)
3. 생성된 이미지를 레퍼런스로 영상 생성 (Seedance / Kling)
4. "keep the same character" 프롬프트 필수 포함
```

### 가상 모델 생성 팁

- **한국인 여성 생성 시 필수**: `"original fictional Korean woman"` 명시
- 그냥 "woman"만 쓰면 서양 모델로 생성됨
- "Korean"만으로 부족한 경우 있음 → "fictional Korean woman" 조합 권장

### 로고 적용 (제품 광고)

- 제품 이미지 + 로고 파일 동시 업로드
- 프롬프트에 반드시 추가: `"do NOT redraw or change the logo, preserve logo exactly"`
- 로고가 변형되는 걸 방지하는 핵심 문구

### 제품 영상 팁

- **제품은 고정, 배경만 애니메이션** → 로고 왜곡 방지
- 병·캔 등 회전시키면 로고가 뒤틀림 → 제품 자체를 움직이지 않는 것이 원칙
- 배경 빛, 파티클, 안개 등을 움직여서 다이나믹한 효과 연출

### 크레딧 상세 (Seedance 기준)

| 해상도 | 길이 | 크레딧 |
|--------|------|--------|
| 1080p | 8초 | 72 크레딧 |
| 4K | 8초 | 176 크레딧 |

- 드래프트는 1080p로 → 최종 확인 후 4K 재생성

### 얼굴 일관성 프롬프트

- 모든 영상 프롬프트에 `"keep the same character"` 포함 필수
- 없으면 씬마다 다른 얼굴로 생성될 수 있음

### 긴 영상 제작 전략

- 8~15초 클립 여러 개 생성 → 영상 편집 툴에서 이어붙이기
- Higgsfield 자체에서 긴 영상 직접 생성보다 클립 단위 조합이 품질 우수

### Marketing Studio / Shorts Studio

- **Marketing Studio**: 제품 광고 전용 UI. 레퍼런스 이미지 + 텍스트 → 자동 광고 생성
- **Shorts Studio**: 숏폼 콘텐츠 자동화. 프리셋 기반으로 배치 생성 가능

### 배치 이미지 생성

- 동일 프롬프트로 여러 변형 이미지 동시 생성 가능
- `generate_image_batch` 사용 → 최적 이미지 선택 후 영상화

### 주의사항

- **모바일 앱 (App Store / Google Play) 비공식** → 반드시 웹 버전 사용
- 비공식 앱은 데이터 탈취 위험 있음

---

## 영상 4: Claude + Higgsfield MCP 수익화 실전
URL: https://youtu.be/OgyotKtYb_4
씬 수: 64개

### SKILL.md 자동 광고 파이프라인

파일명: `AION_Video_Factory_SKILL.md`

```
업로드 → Claude 저장 → /slash 호출
→ 1. 트렌딩 광고 리서치
→ 2. Hook + 아이디어 생성
→ 3. 5가지 유형 콘텐츠 플랜
→ 4. 배치 생성 (20개+)
```

### 광고 5가지 유형

Review / Unboxing / Street Interview / Challenge / ASMR

### 수익화 방법

1. 크몽 영상 제작 서비스: 건당 ~170,000 KRW
2. 자체 브랜드 SNS 마케팅
3. AI 인플루언서 (얼굴 일관성 활용)

### 중요 프롬프트 팁

- **한국 모델 필수 지정**: 기본값은 서양 모델 출력
- 예: `Korean female model, Korean indoor background`
- 안 하면: 서양 배경·모델로 생성됨

### Seedance 업데이트

- Seedance 2.0 → **4K** 지원 (Full HD → 4K 업그레이드)
- Higgsfield에서 "Seedance 2.0 4K" 직접 선택 가능

### 캐릭터 얼굴 일관성

- 다른 씬·스타일에서도 동일 얼굴 유지 가능
- AI 인플루언서 비즈니스의 핵심 기술

### MCP 연결 재확인 (씬 19-26)

```
Claude → Customize → Connectors → + → Custom Connector
Higgsfield MCP URL 붙여넣기 → 이름 'Higgsfield' → Add → Allow
```
연결 완료 후 도구 목록:
Create Voice / Dubbing / Generate 3D / Generate Audio / Generate Image / Generate Video

---

## 영상 3: Higgsfield 실사용자 모델 비교 리뷰
URL: https://youtu.be/oQiKI-DLzVM
씬 수: 58개

### 비디오 모델 성능 순위 (동일 프롬프트 비교)

| 순위 | 모델 | 특징 |
|------|------|------|
| 1 | `seedance_2_5` | 최고 품질. "end-game". 크레딧 높음 |
| 2 | `kling3_0` | I2V·모션 컨트롤 최고. 가성비 우수 |
| 3 | `grok_imagine_2` | 빠른 속도·저비용. 디테일 약간 부족 |
| 4 | `google_veo_3_1_fast` | Kling보다 열세. 오디오 이질감 |
| 5 | `wan_2_7` | **비추천**. 모션 부자연스러움 |

### 이미지 모델 비교

| 모델 | 특징 |
|------|------|
| `gpt_image_2` | 텍스트 정확, 상업용 포스터 최적, 포토리얼 |
| `nano_banana_pro` | 예술적 스타일, 텍스트도 정확 |
| `flux_2_pro` | 의상 디테일 강점 |
| `seedream_5_0_lite` | 텍스트 왜곡 발생 (주의) |

### Higgsfield 가성비 포인트

- Kling을 공식 사이트보다 Higgsfield에서 더 저렴하게 사용 가능
- 플랜에 따라 무제한 생성 가능
- 다른 플랫폼보다 대기열 빠름
- 일괄 다운로드 지원
- 구글 Flow보다 모바일 UX 우수

---



## 영상 1: Higgsfield 기초 사용법
URL: https://youtu.be/VKHOgcHSpsg
씬 수: 50개

### 핵심

**모델 선택**
- `minimax_h3`: 일상 씬, 가성비
- `seedance_2_5`: 복잡·화려한 샷, 최대 30초 롱테이크
- `kling3_0`: 멀티샷, 모션 전이
- `nano_banana_pro`: 4K 이미지
- `gpt_image_2`: 글로벌 1위 이미지 모델

**프롬프트 8요소**
- 이미지 5: Subject · Background · Composition · Lighting · Style
- 영상 추가 3: Camera Move · Subject Motion · Cut Duration
- 오디오 3: BGM · SFX · Dialogue

**기능**
- 이미지: 4K 지원, GPT Image 2 최고 평가
- 영상: Seedance(화려), Minimax(가성비)
- 오디오: QWEN 3.0 (Alibaba) 최고 평가
- 슈퍼컴퓨터: Claude/Gemini로 스토리보드 → 이미지/영상
- 커넥터: TikTok·Instagram 직접 업로드
- MCP/CLI: Claude 채팅에서 직접 Higgsfield 호출
- Academy: 무료 강의 (Movie Making, UGC, Automation)
- 대회: 상금 최대 $1,000,000

**요금제**: Starter $19 / Plus $66 / Ultra $279

---

## 영상 2: Higgsfield MCP × Claude 통합 실전
URL: https://youtu.be/zv0gHwKQT8M
씬 수: 93개

### 3단계 프로덕션 원칙 (핵심!)

```
1. Text (기획) - Claude 기획, 크레딧 0 소모
2. Image (검토) - 이미지로 먼저 확인, 저비용
3. Video (완성) - 최종 영상 생성, 고비용
```
절대 영상부터 바로 생성하지 않는다.

### MCP 연결 방법

1. Higgsfield → MCP → URL 복사
2. Claude.ai → 계정 설정 → Connectors → Add → Custom Connector
3. URL 붙여넣기 → 이름: 'Higgsfield' → 승인

**권한 설정**
| 도구 | 설정 |
|------|------|
| Cancel Auto-renewal | Block (결제 보호) |
| Generate 3D/Audio/Image/Video | Ask Permission (크레딧 관리) |
| Upload Media, Sync Agents | Always Allow |

### 캐릭터 등록 (@me)

1. 셀카 6장 (정면·측면·상하)
2. Higgsfield → Image → GPT Image 2.0 → **4K** 해상도 → 캐릭터 시트 생성
3. Cinema Studio → My Elements → New Element → '@me'
4. Claude 프롬프트: `Me가 주인공, Office가 배경`
5. 배경도 @office 등으로 등록 가능

### Skills (.skll) 시스템

1. .skll 파일 다운로드
2. Claude → 계정 설정 → Skills → Add → Upload Skill
3. `/slash-명령어` 로 호출

**제공 스킬 예시**
| 슬래시 명령 | 기능 |
|------------|------|
| `/higgs-3d-shorts-creator` | 3D 캐릭터 쇼츠 생성 |
| `/higgs-explainer-studio` | 교육 설명 영상 |
| `/higgs-ad-scripter` | 광고 스크립트 + 이미지 (법률 검토 포함) |

### 앱 기능

| 앱 | 용도 |
|----|------|
| Bullet Time Scene | 사진 1장 → 제품 360° 회전 영상 |
| Mixed Media → Canvas | 실제 영상 → 애니메이션/드로잉 스타일 |

### 비용

- 5초 영상 ≈ 50 크레딧
- Claude 기획 단계: 크레딧 0

### 팁

- Claude에 긴 텍스트 붙여넣기: `Ctrl+Shift+V` (서식 없이)
- 이미지 생성은 항상 4K로 (나중에 다운스케일 가능, 반대 불가)
- 드래프트는 저해상도 → 최종만 고성능 모델로
