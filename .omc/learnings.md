# Higgsfield 학습 내용 (영상 분석 기반)

## 외부 소스 학습 2차 (웹 리서치 2026-09 심화)
소스: higgsfield.ai 공식 블로그, claudefa.st, aisuites.ai, workingnotworking.com, aifunnelinsider.com, vo3ai.com 등

### MCP 출시일 및 현황

- **MCP 정식 출시**: 2026년 4월 30일
- **Higgsfield MCP 현재 무료** (free tier 별도)
- 30+ 모델 접근 가능 (2026년 기준, 기존 15개 → 30+으로 대폭 확장)
- Claude Web/Desktop: Settings → Connectors → higgsfield.ai/mcp URL 추가
- Claude Code: `claude mcp add --transport http --scope user higgsfield https://mcp.higgsfield.ai/mcp`

### 2026년 추가된 주요 모델

| 모델 | 특징 | 크레딧/클립 |
|------|------|------------|
| `sora_2` | OpenAI Sora 2 — 최고 품질 | 40~70 크레딧 |
| `veo_3_1` | Google Veo 3.1 — 장면 확장·조명 강점 | ~58 크레딧 (LipSync 1080p) |
| `kling3_0` | 캐릭터·음성 4K — 매우 저렴 | **~6 크레딧** |
| `seedance_2_0` | 네이티브 오디오, 8개 언어 립싱크 | 72 크레딧 (1080p 8s) |
| `wan_2_6` | 리스타일링·리슈팅 전용 | — |
| `minimax_hailuo_2_3_fast` | 속도·비용 우선 | 가장 저렴 |

> **Kling 3.0 주목**: 6 크레딧/클립 → 드래프트는 물론 최종본에도 경제적

### Soul ID — 캐릭터 일관성 솔루션 (신기능)

- **@me 등록 방식 대체**: Soul ID는 별도 학습 기반 캐릭터 고정 시스템
- **학습 사진**: 20~80장 (다양한 각도·조명 권장)
- **효과**: 어떤 스타일·포즈·조명에서도 동일 얼굴 유지
- **적용**: 생성 시 Soul ID 캐릭터 선택 → 프롬프트에 자동 반영
- **Cinema Studio 연계**: Soul ID로 얼굴 고정 + Cinema Studio로 카메라 무브 고정 = 전문 제작 수준

```
Soul ID 설정 → 씬별 카메라 무브 (Cinema Studio 3.5) → 모델 선택 (Seedance/Kling/Veo)
```

### Cinema Studio 3.5 업그레이드

- 가상 카메라 컨트롤이 실제 연출 도구 수준으로 발전
- 독립 리뷰어들이 "단일 모델 플랫폼이 구조적으로 제공할 수 없는 유연성"으로 평가
- Soul ID + Cinema Studio 조합: 하나의 스포크퍼슨이 Seedance 광고 → Kling 내러티브 → Veo 클로즈업 전환 시에도 동일 얼굴·의도된 카메라 무브 유지

### LipSync Studio

- **10개 립싱크 모델** 통합 (저화질 ~ Veo 3.1 고품질까지)
- **다국어 지원**: 녹화 1회 → 영어·스페인어·독일어 등 다국어 버전 자동 생성
- Veo 3.1 LipSync: 1080p 클립당 **58 크레딧**
- Higgsfield Speak (보이스 클론 + 립싱크 동기화)

### Seedance 2.0 네이티브 오디오

- 동일 렌더 패스에서 **음소 단위(phoneme-level) 립싱크** 처리
- **8개 언어** 지원 — 별도 LipSync 단계 불필요
- 멀티샷 내러티브 + 오디오 동기화 → Seedance 2.0 최적

### 2026년 플랜 가격 (업데이트)

| 플랜 | 월 요금 | 크레딧 | 활용 |
|------|---------|--------|------|
| Free tier | $0 | 150 | MCP 테스트용 |
| Starter | $9 | 120 | Kling 2.6 LipSync ~20 클립 |
| Plus | $49 | 1,000 | Veo 3 클립 15~20개 또는 Kling ~100개 |

### 2026 모델별 용도 지침 (업데이트)

| 용도 | 최적 모델 | 이유 |
|------|-----------|------|
| 멀티샷 광고 + 오디오 동기화 | `seedance_2_0` | 네이티브 오디오, 8개 언어 |
| 캐릭터·음성 일관성, 예산 고려 | `kling3_0` | ~6 크레딧/클립, 4K 지원 |
| 일상·단기 숏폼·드래프트 | `minimax_hailuo_2_3_fast` | 가장 빠르고 저렴 |
| 최고 품질 시네마틱 | `sora_2` or `veo_3_1` | 40~70 크레딧/클립 |
| 비추천 | `wan_2_7` | 모션 부자연스러움 (wan_2_6은 리스타일 전용) |

### GitHub 커뮤니티 리소스

- **[AKCodez/higgsfield-claude-skills](https://github.com/AKCodez/higgsfield-claude-skills)**: 19개 Claude Code 스킬
  - 이미지 생성, Seedance 2.0 영상, UGC 광고 파이프라인 자동화
  - Playwright 브라우저 자동화 포함

### Higgsfield CLI

- `higgsfield.ai/cli` — 터미널에서 직접 명령어로 생성 가능
- Claude Code와 병행하여 스크립트 자동화에 활용 가능

---

## 외부 소스 학습 (웹 리서치 2026-09)
소스: higgsfield.ai 공식 블로그, Medium, techsy.io, conceptbeans.com, digen.ai, Wikipedia 등

### MCP 설치 원라인 명령 (Claude Code)

```bash
claude mcp add --transport http --scope user higgsfield https://mcp.higgsfield.ai/mcp
```
- API 키 불필요 — OAuth로 Higgsfield 계정 연동
- 60초 이내 설치 완료
- **무료 티어**: 월 150 크레딧 (카드 불필요)

### 회사 현황 (2026)

- 2026년 1월: Series A 라운드 $8,000만 달러 추가 유치
- 기업가치 **$13억 달러(≈ 1.3B)** 이상
- 2025년 3월: 브라우저 기반 엔드-투-엔드 AI 영상 제작 플랫폼 출시

### 신기능: Popcorn (AI 스토리보드)

- 사진 최대 **4장** 동시 입력 (캐릭터 + 배경 + 오브젝트 + 무드 레퍼런스)
- 씬 간 **캐릭터·조명·환경 일관성** 자동 유지
- Sora 2로 원클릭 내보내기 지원
- 영상 생성 전 스토리보드로 구도·순서 먼저 확정하는 데 사용

### 신기능: Hook Generator

- 제품/서비스 정보 입력 → AI가 **3~5개 바이럴 훅 아이디어** 자동 제안
- 2026년 트렌드 기반 고참여율 콘셉트 생성
- Marketing Studio 내 통합

### Seedance 프롬프트 4요소 구조 (공식 가이드)

```
① 피사체 동작 → ② 배경·조명 → ③ 카메라 무브 → ④ 분위기·무드
```

**카메라 무브 직접 인식 키워드:**
`dolly in` / `truck left` / `arc shot` / `push in` / `pull back wide`
`handheld follow` / `crane up` / `orbital move`

### 레퍼런스 이미지 활용 (@태그 시스템)

- `@파일명` 태그로 업로드한 이미지를 **생성 제약(constraint)**으로 적용
- 단순 참고가 아닌 강한 구속력 → 얼굴·제품 일관성에 효과적
- 일부 모델에서 레퍼런스 이미지 **최대 9장** 동시 입력 가능

### 드래프트 검증 전략 (크레딧 절약)

- 1080p 생성 전 **720p로 먼저 검증** → 모션 로직·카메라·구도 확인
- 720p에서 구도 확정 후 최종만 1080p/4K 재생성

### 배치 생성 프리셋

| 프리셋 | 용도 |
|--------|------|
| UGC | 사용자 생성 콘텐츠 스타일 |
| TV Spot | 방송 광고 형식 |
| Wild Card | 자유 형식 |

- 브랜드 킷으로 렌더 간 일관성 유지
- 하나의 프롬프트 → 여러 플랫폼 사이즈로 팬아웃 가능

### 종합 워크플로우 팁

- **프롬프트 템플릿 라이브러리 구축**: 잘 작동한 프롬프트를 저장해 자산화
- **플랫폼별 비율 명시 필수**: 16:9 vs 9:16 — 틀리면 크레딧 낭비
- **반복 개선**: 첫 결과물은 최종본이 아님. "뭐가 다른지" 서술 후 재생성
- **Claude로 프롬프트 초안 작성**: 아이디어를 평문으로 설명 → Claude가 영상 프롬프트로 변환

### 수익 사례

- Claude + Higgsfield MCP 콘텐츠 에이전시로 **월 $10,000** 달성 사례 (Medium 보고)
- 크리에이티브 마케팅 에이전시 자동화 파이프라인

---

## 영상 6: Seedance 2.5 출시 홍보 영상 (플레이리스트)
URL: https://youtube.com/playlist?list=PLOL0MpbH6W5w
씬 수: 5개 (35초 쇼츠 형식)

### Seedance 2.5 (`seedance_2_5`) 주요 업그레이드

| 항목 | 2.0 | 2.5 |
|------|-----|-----|
| 해상도 엔진 | 720p 수준 | 1080p (선명도 대폭 향상) |
| 패브릭 물리 | 뭉개짐 | 의상 주름·움직임 자연스러움 |
| 배경 왜곡 | 발생 | 없음 (structural integrity 유지) |
| 색감 | 보통 | 더 선명한 채도·대비 |

### 모션 컨트롤 슬라이더 (신기능)

- **Speed** 슬라이더: 움직임 속도 조절
- **Intensity** 슬라이더: 움직임 강도 조절
- 이미지 업로드 후 두 슬라이더로 AI 모션 세밀 조정 가능

### 주요 활용 사례 (씬 4 몽타주)

1. **하이패션 프로모**: 네온 사이버펑크 런웨이 모델 워킹
2. **제품 광고**: 커피 슬로모션 투명 유리 포어링 (리퀴드 스플래시)
3. **건축 시각화**: 현대 빌라 3D 렌더 + 나무 흔들림 자연스럽게

### 콘텐츠 구조 (UGC 쇼츠 패턴)

```
Opening Hook (0~5초) → 제품 비교 (5~13초) → 기능 설명 (13~21초)
→ 활용 사례 몽타주 (21~29초) → Call to Action (29~35초)
```
- 35초 이하 숏폼 광고에 최적화된 5씬 구조

---

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
