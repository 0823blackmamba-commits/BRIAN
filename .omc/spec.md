# video-shot-agent 스펙

## 목적
레퍼런스 영상(YouTube URL 또는 업로드 파일)을 씬 단위로 분석한 뒤,
각 샷을 Higgsfield API로 재생성하는 Claude Code 슬래시 스킬.

## 핵심 흐름

```
입력(YouTube URL / 업로드) → video_analysis_create
  → 폴링(video_analysis_status) → scenes[] 파싱
  → 프롬프트 설계 → generate_video_batch
  → jobs_wait 폴링 → show_generation_by_ids
```

## 사용 도구 (확정)

| 역할 | 도구명 |
|------|--------|
| 업로드 (위젯) | mcp__Higgsfield__media_upload_widget |
| URL 임포트 | mcp__Higgsfield__media_import_url |
| 영상 분석 시작 | mcp__Higgsfield__video_analysis_create |
| 분석 상태 조회 | mcp__Higgsfield__video_analysis_status |
| 단일 영상 생성 | mcp__Higgsfield__generate_video |
| 배치 영상 생성 | mcp__Higgsfield__generate_video_batch |
| 생성 대기 | mcp__Higgsfield__jobs_wait |
| 결과 표시 | mcp__Higgsfield__show_generation_by_ids |

## 기본 모델

- 일반 씬: `seedance_2_5`
- 멀티샷 / 모션 전이: `kling3_0`

## Tier 정의

- Tier 1: 분석만 (씬 목록 출력)
- Tier 2: 씬 1개 end-to-end 검증 ← **기본**
- Tier 3: 전체 씬 생성

## 제약

- 생성 전 씬 목록 및 수량 확인 필수
- use_unlim은 명시적 요청 시만 true
- 12개 초과 씬은 그룹 처리
