# video-shot-agent 진행 상황

## 현재 상태: SKILL.md 완성, Tier 2 검증 대기

## 완료
- Higgsfield 도구 목록 세션에서 직접 확인 및 SKILL.md에 반영
- SKILL.md 작성 완료 → `.claude/skills/video-shot-agent/SKILL.md`
- 추적 파일 생성 (.omc/spec.md, task_plan.md, progress.md)

## 다음 행동

1. **레퍼런스 영상 링크 제공** → Tier 2 end-to-end 검증 실행
   - YouTube URL을 이 세션에 붙여넣기
   - 또는 영상 파일 첨부 (media_upload_widget 자동 실행)

2. 검증 흐름:
   - video_analysis_create → 씬 분석
   - scenes[0] 하나로 generate_video
   - 결과 확인 후 Tier 3 진행 여부 결정

## 도구명 (확정)

| 역할 | 확정된 도구명 |
|------|--------------|
| 업로드 위젯 | mcp__Higgsfield__media_upload_widget |
| URL 임포트 | mcp__Higgsfield__media_import_url |
| 분석 시작 | mcp__Higgsfield__video_analysis_create |
| 분석 조회 | mcp__Higgsfield__video_analysis_status |
| 단일 생성 | mcp__Higgsfield__generate_video |
| 배치 생성 | mcp__Higgsfield__generate_video_batch |
| 대기 | mcp__Higgsfield__jobs_wait |
| 표시 | mcp__Higgsfield__show_generation_by_ids |
