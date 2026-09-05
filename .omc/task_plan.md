# video-shot-agent 태스크 플랜

## 완료된 작업

- [x] Higgsfield 실제 도구 목록 확인 (세션에서 직접 스키마 로드)
- [x] SKILL.md 작성 (`/.claude/skills/video-shot-agent/SKILL.md`)
- [x] spec.md, task_plan.md, progress.md 생성

## 남은 작업

- [ ] **Tier 2 end-to-end 검증**: 레퍼런스 영상 1개로 전체 흐름 실행
  1. YouTube URL 입력
  2. video_analysis_create 호출
  3. video_analysis_status 폴링 → 완료 대기
  4. scenes[0] 하나로 generate_video 호출
  5. jobs_wait → show_generation_by_ids
  6. 결과 확인

- [ ] 검증 완료 후 Tier 3 (전체 씬) 실행 여부 사용자 결정

## 브랜치

`claude/video-shot-agent-execution-1hiamv`
