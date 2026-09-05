# Higgsfield 학습 내용 (영상 분석 기반)

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
