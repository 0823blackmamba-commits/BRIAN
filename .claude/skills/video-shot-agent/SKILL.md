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
- 기본 모델: `seedance_2_5` (일반 영상) / `kling3_0` (멀티샷·모션 전이)

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
