
# AI 활용 포트폴리오 (김성진)

### 프로젝트 A: 개발한입
- **해당 항목**: ①AI 활용 자동화 사례, ②프롬프트 템플릿
- **핵심 성과**: 12,400개 콘텐츠 자동 생성, 생산성 99% 향상

### 프로젝트 B: 갈라쇼  
- **해당 항목**: ⑥프로토타입 제작
- **핵심 성과**: 72시간 만에 MVP 완성, AI 기여도 86%

### 프로젝트 C: ifland
- **해당 항목**: ⑤AI의 한계와 해결	
- **핵심 성과**: 에러 분석 90% 시간 단축, 개발 생산성 85% 향상

---

# 프로젝트 A: 개발한입 (숏폼 학습 플랫폼)
10-25초 분량의 숏폼으로 개발 지식을 학습하는 마이크로러닝 플랫폼  
**기간**: 2025.11 ~ 2026.01 (3개월) | **팀**: 2인 개발

### 역할 및 기여도
| 영역 | 본인 기여도 | AI 활용 |
|------|------------|---------|
| 서비스 기획 | 90% | - |
| **AI 파이프라인 설계** | **100%** | Claude API 활용 |
| 프론트엔드 개발 | 100% | - |
| 백엔드 개발 | 0% | Springboot/Lambda(팀원) |
| **UI/UX 디자인** | **100%(AI 70%)** | **Google Stitch** |
| 인프라 구축 | 100% | - |

### 기술 스택 & 링크
- **AI/LLM**: Claude API (Sonnet 4.5), 프롬프트 엔지니어링
- **Frontend**: React, TypeScript, PWA
- **Infrastructure**: AWS (S3, CloudFront, Route53)
- **라이브**: https://devonebite.xyz
- **GitHub**: [Client](https://github.com/Guui-Developer/Dev_OneBite) | [Admin](https://github.com/Guui-Developer/Dev_OneBite_Admin)

---

## ① AI를 활용해 해결한 문제/자동화 - 12,400개 콘텐츠 자동 생성

### 문제 상황
개발한입 프로젝트는 개발자들이 출퇴근 시간이나 짧은 휴식 시간에 빠르게 지식을 습득할 수 있도록 돕는 서비스입니다. 이를 위해 대량의 콘텐츠가 필요했습니다.

62개 기술 카테고리에 각 200개씩 **총 12,400개 콘텐츠**를 생성해야 했습니다. 각 콘텐츠는 5가지 타입(code_tip, bug_challenge, interview, code_review, meme)으로 구성됩니다.

**전통적인 방식의 한계**

| 항목 | 수치 |
|------|------|
| 1개 콘텐츠 작성 시간 | 10분 |
| 총 소요 시간 (12,400개) | 2,067시간 |
| 2인 팀 작업 기간 | **약 260일 (1년)** |
| 예상 인건비 (시간당 5만원) | 약 1억 340만원 |

**추가 문제점**
- **품질 일관성**
	- 작성자 컨디션에 따라 톤앤매너, 난이도가 불일치
- **지속 가능성**
	- 정기 업데이트 및 최신 트렌드 반영 불가능


### AI 활용 방법

#### 1단계: 모델 선정

| 모델 | 장점 | 단점 | 선택 |
|------|------|------|------|
| GPT-4o | 빠른 속도 | 일관성 부족, 한국어 톤 부정확 | ❌ |
| **Claude Sonnet 4.5** | **한국어 자연스러움, 높은 일관성** | 비용 높음 | ✅ |
| Gemini 3 | 최신 LLM | 일관성 부족 | ❌ |

**선정 이유**: "~해요", "~이에요" 같은 세밀한 한국어 톤 제어가 가능하고, JSON 스키마 준수율 95% 이상으로 안정적

#### 2단계: 프롬프트 엔지니어링 (반복 개선)

**개선 과정**

```
1차 (60% 정확도) - 단순 지시
→ 형식 불일치 40%, 길이 무시 30%

2차 (80% 정확도) - 구조화된 지시
→ 100개 샘플 분석, 예시 3개 추가
→ 여전히 톤앤매너 불일치 15%

3차 (95~99% 정확도) - 계층적 프롬프트
→ Base Prompt + Type Prompt + 강조 지시문
→ 500개 샘플 검증
```

### 개선 결과

| 지표 | Before (수동) | After (AI) | 개선률 |
|------|--------------|-----------|--------|
| **생산성** |||
| 1개 생성 시간 | 10분 | 6초 | **99.0%** ↓ |
| 전체 소요 시간 | 2,067시간 | 20시간 | **99.0%** ↓ |
| 2인 팀 작업 기간 | 260일 | 3일 | **98.8%** ↓ |
| **비용** |||
| 총 비용 | 1억+ | 120만원 | **99.0%** ↓ |
| **품질** |||
| 톤앤매너 일관성 | 60% | 95% | **58%** ↑ |
| 형식 정확도 | 80% | 98% | **23%** ↑ |

---

## ② 실제 사용한 프롬프트 템플릿

### 프롬프트 구조

```
Base Prompt (공통 규칙, 2,000 토큰)
+ Type Prompt (타입별 규칙, 500 토큰)  
+ 강조 지시문 (절대 규칙, 300 토큰)
```

### Prompt (핵심만 발췌)

```markdown
당신은 개발자를 위한 숏폼 학습 콘텐츠를 생성하는 AI입니다.

# 필수 준수 사항

## 1. 태그 규칙 (매우 중요!)
**사용 가능한 태그**: javascript, typescript, python, react, vue, 
docker, aws, algorithm, datastructure 등 62개

⚠️ **공통 카테고리 특별 규칙**
datastructure, algorithm, os, network, databasetheory는 
반드시 단독 태그로만 사용. 다른 태그와 조합 불가.

올바른 예시:
- {"tags": ["javascript", "react"]} ✅
- {"tags": ["algorithm"]} ✅

잘못된 예시:
- {"tags": ["algorithm", "javascript"]} ❌

## 2. 콘텐츠 길이 제한
- title: 18자 이내 (이모지 포함)
- description: 40-50자
- code: 각 줄 40자 이내, \n으로 줄바꿈

## 3. 톤앤매너
- code_tip: 친근하고 실용적 ("~해요", "~이에요")
- interview: 전문적이고 정확하게 ("~입니다")
- code_review: 건설적이고 교육적 ("~하면 더 좋아요")
```

### Type-specific Prompt 예시 (code_tip만)

```markdown
다음 형식의 JSON으로 code_tip 콘텐츠를 생성해줘:

{
  "type": "code_tip",
  "title": "[이모지] [핵심 키워드, 18자 이내]",
  "code": "[1-3줄, \\n으로 줄바꿈]",
  "language": "[javascript|python 등]",
  "description": "[40-50자, 한 문장]",
  "tags": ["태그1", "태그2"]
}

조건:
- 기술 스택: {CATEGORY}
- 난이도: 초급
- 실무 팁 위주
- 학습 시간: 10-15초

예시:
{
  "type": "code_tip",
  "title": "💡 구조 분해 할당으로 변수 교환",
  "code": "let a = 1, b = 2;\\n[a, b] = [b, a];",
  "language": "javascript",
  "description": "임시 변수 없이 두 변수 값을 바꿀 수 있어요.",
  "tags": ["javascript", "es6"]
}
```

### 프롬프트 개선 과정 (초안 → 최종)

**초안 (1차, 정확도 60%)**
```markdown
JavaScript 코드 팁 10개를 JSON으로 만들어줘
```
**문제점**: 형식 불일치 40%, 길이 무시 30%, 태그 오류 30%

---

**개선 1차 (2차, 정확도 80%)**
```markdown
다음 JSON 형식으로 JavaScript code_tip 10개 생성:
- title: 18자 이내
- description: 40-50자
- tags: javascript, typescript 등에서 선택

예시 3개 포함
```
**개선**: 필드 정의 명시, 예시 추가  
**문제점**: 여전히 톤앤매너 불일치 15%, 공통 카테고리 규칙 위반 5%

---

**최종 (3차, 정확도 95~99%)**
```markdown
[Base Prompt 2,000토큰]
+ [Type Prompt 500토큰]
+ [강조 지시문]
  ⚠️ 40자 미만은 자동 거부됩니다
  🚨 공통 카테고리는 단독 태그만
  ✅ 태그는 여러 개 가능
```
**개선**: 계층적 구조, 강조 표현, 체크리스트  
**효과**: 형식 정확도 98%, 재생성 0.5회/개

### 대량 생성 후 발견된 문제

100개 샘플 생성 후 자동 검증 결과:
- ✅ 통과: 65개 (65%)
- ❌ 실패: 35개 (35%)

**실패 원인 분석**

| 원인 | 개수 | 비율 |
|------|------|------|
| description 길이 부족 (40자 미만) | 20개 | 57% |
| code 포매팅 오류 (들여쓰기 등) | 12개 | 34% |
| 톤앤매너 불일치 ("~합니다" 사용) | 5개 | 14% |
| meme 이미지 URL 무효 (환각) | 15개 | 43% |

### 문제 1: description 길이 부족

**AI 초안**
```json
{
  "description": "at() 메서드로 음수 인덱스 사용이 가능해요"
  // 길이: 24자 (목표: 40-50자)
}
```

**최종 수정본**
```json
{
  "description": "at() 메서드로 음수 인덱스를 사용해 배열 끝에서부터 접근할 수 있어요"
  // 길이: 45자 ✅
}
```

**해결**: 프롬프트에 "⚠️ 40자 미만은 자동 거부" 강조 추가

### 문제 2: 톤앤매너 미세 조정

**AI 초안 (부정적 표현)**
```json
{
  "type": "code_review",
  "feedback": "> Object.assign은 구식이에요. 스프레드를 쓰세요"
}
```

**최종 수정본**
```json
{
  "feedback": "> 스프레드 연산자가 더 직관적이고 읽기 쉬워요"
}
```

**해결**: code_review 톤 가이드에 "부정 표현 금지" 명시

### 문제 3: 환각 - 존재하지 않는 이미지 URL

**AI 초안**
```json
{
  "type": "meme",
  "image": "https://i.imgflip.com/2/5c7lwq.jpg"
  // 실제로 존재하지 않는 URL
}
```

**검증 결과**: 20개 meme 중 15개 URL 무효 (75% 환각)

**해결**: 프롬프트 수정으로 이미지 URL 대신 설명 생성하도록 하여 해결했습니다

### 전체 개선 결과

```
초기 생성: 100개
→ 자동 검증 통과: 65개 (65%)
→ 프롬프트 개선 후 재생성: 35개
→ 재생성 후 통과: 33개 (94%)
→ 수동 수정: 2개 (6%)

최종 결과: 98개 자동 생성 성공 (98%)
```

| 항목 | 1차 생성 | 개선 후 | 향상 |
|------|---------|--------|------|
| description 길이 준수 | 65% | 95% | **46%** ↑ |
| code 포매팅 정확도 | 88% | 98% | **11%** ↑ |
| 톤앤매너 일관성 | 95% | 100% | **5%** ↑ |
| **전체 성공률** | **65%** | **98%** | **51%** ↑ |

---

### 3단계 품질 관리 시스템

```
1️⃣ 자동 검증 (100% 검사)
   ✅ JSON Schema, 길이, 태그 규칙
   → 통과율 95%

2️⃣ 샘플링 검수 (20% 추출)
   ✅ 톤앤매너, 내용 정확성, 학습 가치
   → 검수자 2명 교차 검증

3️⃣ 사용자 피드백 (운영 단계)
   → 싫어요 문의시 재생성
```

### 효과

| 지표 | Before | After | 개선 |
|------|--------|-------|------|
| 검수 시간 | 3분/개 | 10초/개 | **95%** ↓ |
| 검수 일관성 | 70% | 98% | **40%** ↑ |
| 재작업율 | 30% | 5% | **83%** ↓ |

---

# 프로젝트 B: 갈라쇼 (스트리밍 파티 게임)
스트리머와 시청자가 실시간 채팅으로 함께 즐기는 인터랙티브 파티 게임  
**기간**: 2025.07 ~ 진행 중 | **팀**: 1인 개발
### 역할 및 기여도

| 영역 | 본인 기여도 | AI 활용 |
|------|-----------|---------|
| **아키텍처 설계** | **20%** | **Claude Opus 4.5 (80%)** |
| Unity 클라이언트 | 70% | Meshy.ai 3D 에셋 (30%) |
| React 클라이언트 | 55% | Claude Code CLI (45%) |
| 백엔드 API | 30% | Claude Code CLI (70%) |
| 채팅 라이브러리 | 40% | Gemini 문서 분석 (60%) |
| 인프라 | 100% | - |

### 기술 스택 & 링크
- **AI Tools**: Claude Opus 4.5, Meshy.ai, Claude Code, Gemini
- **Tech**: Unity WebGL, React, .NET, AWS Lambda
- **GitHub**: [Client](https://github.com/Thedum2/GalaShow_Client) | [Unity](https://github.com/Thedum2/GalaShow_Unity) | [API](https://github.com/Thedum2/GalaShow_API)
- **npm**: [polychat-bridge](https://www.npmjs.com/package/polychat-bridge)

---

## ⑥ AI를 활용한 프로토타입 제작 - 72시간만에 만든 MVP

### 프로젝트 배경
혼자서 **기획-디자인-프론트엔드-백엔드-게임 개발**을 모두 담당해야 하는 상황에서, 전통적인 방식으로는 최소 1년 이상이 예상되었습니다. 특히 3D 에셋 제작과 화면 디자인은 외주 의뢰 없이는 불가능해 보였습니다.  
  
_AI를 파트너로 활용하면 어디까지 가능할까? 라는 고민과 함께_ **_프로토타입의 제작으로 빠른 시장 반응_**_을 보고 싶었습니다._

**범위**
- ✅ Unity 미니게임 1개
- ✅ React 스트리머 UI / Admin UI
- ✅ Twitch 채팅 연동
- ✅ 기본적 게임 API제작

**태스크**
- Unity WebGL + React 통신
- 5개 독립 레포지토리 연결
- 확장 가능한 미니게임 프레임워크

### AI 활용 전략 
**Claude Opus 4.5로 아키텍처 설계**

```markdown
다음 요구사항을 만족하는 시스템 아키텍처를 3가지 안으로 제시해줘:

**요구사항**
- Unity WebGL 게임 엔진
- React 스트리머 제어 UI
- 5개 스트리밍 플랫폼(Twitch, YouTube, 아프리카TV, 치지직, 카카오TV) 채팅 통합
- 백엔드 API (.NET)
- Admin 관리 페이지

**제약사항**
- 1인 개발
- 72시간 내 프로토타입
- 향후 확장 가능해야 함

각 안마다 다음을 포함:
1. 레포지토리 구조
2. 장점 3가지
3. 단점 3가지
4. 예상 개발 시간
5. 확장성 평가 (5점 만점)

```

**Claude 제안**: 모노레포, 멀티레포, 하이브리드 3가지 안 제시  
**최종 선택**: 멀티레포
**효과**: 아키텍처 설계 4시간 → 30분으로 단축

**React <->Unity** 간 통신 프로토콜 설계
```
[프롬프트] 
React WebApp에 Unity WebGL을 임베드하고 양방향 통신하는 시스템을 설계해줘. 
보안, 성능, 확장성 측면에서 트레이드오프 분석 포함.
```
**생성 결과**:


**Meshy.ai로 3D 에셋 자동 생성**
```
[프롬프트]
Create a 3D model of a vintage trolley train 
for a moral dilemma game. Low poly style.
```

**생성 결과**:
- 트롤리 모델: 정점 500개, 폴리곤 300개
- 텍스처: 512x512
- 소요 시간: **5분** (직접 모델링 시 2주 예상)

**Gemini로 API 문서 분석**
```markdown
[프롬프트]
Twitch, YouTube, 아프리카TV 채팅 API 문서 비교하고
공통 인터페이스 설계해줘
[링크]
[링크]
[링크]
```
**Gemini 제안** (80% 채택):
```typescript
interface ChatAdapter {
  connect(): Promise<void>;
  onMessage(callback: (msg: ChatMessage) => void): void;
}
```
---

### AI별 기여도

| AI 도구 | 사용 시간 | 주요 용도 |
|---------|----------|---------------|--------|----------|
| Claude Opus 4.5 | 2시간 | 아키텍처 |
| Claude Code | 8시간 | 핵심 로직 구현|
| Meshy.ai | 1시간  | 3D 에셋 |
| Gemini | 3시간  | API 문서 분석 및 인터페이스 생성 |
| **합계** | **14시간**  | - |

### 개발 시간 분석
```
총 개발 시간: 68시간 (목표 72시간, 6% 단축)

AI 절약 시간:
- 아키텍처 설계: 4h → 0.5h (3.5h 절약)
- 3D 에셋 제작: 336h → 1h (335h 절약)
- 보일러플레이트: 10h → 2h (8h 절약)
- API 문서 분석: 8h → 1h (7h 절약)

총 절약: 약 354시간
AI 없이 예상: 약 420시간 (10.5주)
```
---

## ⑦ LLM 기반 기능 개발 - 멀티 플랫폼 채팅 통합 라이브러리

스트리머들이 플랫폼 선택 고민으로 멀티 스트리밍을 하면서 발생하는 채팅 분산 문제를 해결하기 위해 만들었습니다.  
각 플랫폼마다 채팅 API 방식이 다르고,제약이 다르기 때문에, 하나하나 구현하기에도 무리가 있다고 판단해서,모든 플랫폼 채팅을 **하나의 통일된 방식으로 받을 수 있는 어댑터 라이브러리를 제작**했습니다.

**기술 스택**
- LLM: Gemini (API 문서 분석)
- 통합 대상: , YouTube, 치지직, SOOP

### 구현 과정

#### 1. API 문서 분석 (Gemini 활용)

```markdown
[프롬프트 to Gemini]
다음 3개 플랫폼의 채팅 API 비교:
1. Twitch Chat API [문서 URL]
2. YouTube Live Chat API [문서 URL]  
3. 아프리카TV 채팅 API [문서 URL]

공통점과 차이점을 표로 정리하고,
TypeScript 어댑터 인터페이스 제안해줘.
```

**Gemini 분석 결과** (처리 시간: 1시간 → 10분)

| 플랫폼 | 연결 방식 | 메시지 형식 | 인증 |
|--------|----------|------------|------|
| CHZZK| WebSocket | JSON | OAuth |
| YouTube | HTTP Polling | JSON | API Key |
| SOOP(아프리카TV) | WebSocket | JSON | Session |

**공통 인터페이스 제안** (80% 채택):
```typescript
interface ChatAdapter {
  connect(): Promise<void>;
  disconnect(): Promise<void>;
  onMessage(callback: (msg: ChatMessage) => void): void;
  sendMessage(text: string): Promise<void>;
}

interface ChatMessage {
  id: string;
  username: string;
  message: string;
  timestamp: number;
  platform: 'twitch' | 'youtube' | 'afreeca';
}
```
### 성과

- 문서 분석 시간: 8시간 → 1시간 (87% 단축)
- 통합 작업 시간: 1주예상→ 2일 (71% 단축)
- API 호출 비용: 60% 절감
- npm 패키지로 공개 (https://www.npmjs.com/package/polychat-bridge)
- 재사용 가능한 인터페이스 확립

---

# 프로젝트 C: ifland (메타버스 플랫폼)
> ⚠️ **주의**: 본 섹션은 개인 업무 효율화 사례입니다. 회사 공식 AI 도입 사례가 아닙니다.

SK텔레콤의 소셜 메타버스 플랫폼 **ifland** 클라이언트 개발에 참여했습니다. 사용자가 아바타를 커스터마이징하고 가상 공간에서 파티, 세미나, 공연 등 다양한 활동을 즐길 수 있으며, NFT 기반 아이템과 후원 기능 등 경제 시스템을 갖춘 플랫폼입니다.
**기간**: 2022.06 ~ 2024.10 (2년 5개월) | **팀**: 클라이언트 개발팀

### 역할 및 기여도

| 영역 | AI 활용 (개인) |
|------|-----------|---------------|
| Unity 클라이언트 개발 |ChatGPT |
| 볼류메트릭 콘서트 | **ChatGPT  (로그 분석)** |
| AI 페르소나 NPC |**ChatGPT (API 분석)** |
| 성능 최적화 | ChatGPT |

### 기술 스택
- **Game Engine**: Unity, C#
- **External**: Microsoft MRCS (Volumetric Video), AI Persona Engine
- **AI Tools**: GitHub Copilot, ChatGPT, Claude (개인 업무 효율화)

### 성과
- 누적 다운로드 **870만 건**
- 제휴 요청 **2,000건 이상**
- 최대 **131명 동시 참여** 지원
---

## ⑤ AI의 한계를 겪고 해결한 경험 :  환각(hallucination) 문제

### 활용 배경

대규모 코드베이스(50만+ 라인)에서:
- ❌ 신규 태스크로서 코드베이스 파악에 시간 소요
- ❌ 에러 로그 분석 어려움 (50줄 이상 스택 트레이스)
- ❌ 외부 라이브러리 영문 문서 이해 시간 소요

### 사례 1: 에러 로그 분석 - AI 환각 문제 발견 및 해결

**문제 상황**

Microsoft MRCS(Mixed Reality Capture Studios) 통합 중 알 수 없는 에러 발생. 50줄 이상의 스택 트레이스로 원인 파악 어려움.

```
[ERROR] MRCSStreamingException: Failed to initialize volumetric stream
at Microsoft.MixedReality.Streaming.VolumetricStreamManager.Initialize()
at IflandMetaverse.Features.Concert.VolumetricConcertController.StartStream()
... (50줄 이상)
```

**AI 활용 (Claude)**

```markdown
[프롬프트 to Claude]
다음 에러 로그를 분석해줘. 원인과 해결 방법을 제시해줘:

[에러 로그 전체 붙여넣기]

참고: Microsoft MRCS Unity SDK 사용 중
```

**Claude 응답**

```markdown
가능한 원인 3가지:
1. 네트워크 연결 문제 → 방화벽 설정 확인
2. 라이선스 인증 실패 → API Key 확인
3. Unity WebGL 플랫폼 미지원 → 플랫폼 확인

디버깅 순서:
1. Debug.Log로 apiKey 출력
2. Ping으로 MRCS 서버 연결 확인
3. Unity 플랫폼 확인
```

**환각 문제 발견**

Claude 제안대로 순차적으로 확인했으나:

-   ✅ 1번: 방화벽 정상, 네트워크 연결 문제 없음
-   ✅ 2번: API Key 정상 인증
-   ✅ 3번: Unity 플랫폼 확인 → **WebGL에서 Android로 변경 → 정상 작동!**

**하지만 추가 환각 발견**: Claude가 "MRCSConfig.EnableAutoRetry()"라는 존재하지 않는 API를 제안


```markdown
[Claude의 추가 제안]
"MRCSConfig.EnableAutoRetry()를 true로 설정하면
연결 실패 시 자동으로 재시도합니다."
```

**검증 결과**: Microsoft MRCS 공식 문서에 해당 API 없음 (환각 발생)

**해결 과정: 3단계 검증 시스템 구축**

```
1️⃣ AI에게 질문 (개선된 프롬프트)
   → Unity/MRCS 버전 명시
   → 공식 문서 URL 요구

2️⃣ 자동 검증
   → Microsoft MRCS 공식 문서 검색
   → Unity Forum 검색
   → GitHub Issues 검색

3️⃣ 실제 테스트
   → Unity Editor에서 API 존재 확인
   → 테스트 빌드
   → 실행 검증
```

**개선된 프롬프트**


```markdown
Microsoft MRCS Unity SDK 1.2.3 기준으로 
다음 에러 해결 방법 알려줘:

[에러 로그]

⚠️ 제약사항:
- Microsoft MRCS 공식 문서에 명시된 API만 사용
- 각 해결 방법마다 공식 문서 URL 첨부

출력 형식:
1. 방법: [정확한 API/설정]
2. 문서: [URL]
3. 주의사항: [있다면]
```

**효과**

-   환각 발생률: 30% → 0%
-   에러 분석 시간: 3시간 예상 → **20분 해결 (90% 단축)**
-   신뢰도: 검증된 해결책만 제시

### 정량적 성과

| 활용 사례 | Before | After | 절감 시간 |
|----------|--------|-------|----------|
| 에러 로그 분석 | 3시간 | 20분 | 2시간 40분 |
| 반복 코드 작성 | 5시간 | 1시간 | 4시간 |
| API 문서 이해 | 8시간 | 1시간 | 7시간 |
| **총계** | **16시간** | **2시간 20분** | **13시간 40분** |

**개발 생산성 향상**: 약 **85%**
