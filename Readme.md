
# AI 활용 포트폴리오 (김성진)

### 프로젝트 A: 개발한입
- **해당 항목**: ①AI 활용 자동화 사례, ②프롬프트 템플릿
- **핵심 성과**: 12,400개 콘텐츠 자동 생성, 생산성 99% 향상

### 프로젝트 B: 갈라쇼  
- **해당 항목**: ⑥프로토타입 제작
- **핵심 성과**: 72시간 만에 MVP 완성, AI 기여도 86%

### 프로젝트 C: ifland
- **해당 항목**: ⑤AI의 한계와 해결	
- **핵심 성과**: 에러 분석에 필요한 시간 50% 이상 단축

---

# 프로젝트 A: 개발한입 (숏폼 학습 플랫폼)
<img width="2353" height="1310" alt="Frame 3 (1)" src="https://github.com/user-attachments/assets/b3ee18d7-5e2c-40ef-bdc4-d992603f0ddb" />
10-25초 분량의 숏폼으로 개발 지식을 학습하는 마이크로러닝 플랫폼

#### **💻서비스 링크**: https://devonebite.xyz

* **기간**: 2025.11 ~ 2026.01 (3개월)
* **팀**: 2인 개발

### 역할 및 기여도
| 영역 | 본인 기여도 | AI 활용 |
|------|------------|---------|
| 서비스 기획 | 100% | - |
| **콘텐츠 생성/검증 AI 파이프라인 설계** | **100%** | Claude API 활용 |
| 프론트엔드 개발 | 100% | - |
| 백엔드 개발 | 0% | Springboot/Lambda(팀원) |
| **UI/UX 디자인** | **100%(AI 70%)** | **Google Stitch** |
| 인프라 구축 | 100% | - |

### 기술 스택 & 링크
- **AI/LLM**: Claude API (Sonnet 4.5), 프롬프트 엔지니어링
- **Frontend**: React, TypeScript, PWA
- **Infrastructure**: AWS (S3, CloudFront, Route53)
- **GitHub**: [Client](https://github.com/Guui-Developer/Dev_OneBite) | [Admin](https://github.com/Guui-Developer/Dev_OneBite_Admin)

---

## ① AI를 활용해 해결한 문제/자동화 - 12,400개 콘텐츠 자동 생성
<img width="503" height="797" alt="image" src="https://github.com/user-attachments/assets/56574500-40f3-4e3b-8a40-8e62ba266706" />

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
	- 작성자 컨디션에 따라 톤앤매너, 난이도등 퀄리티의 일정함이 없음
- **지속 가능성**
	- 정기 업데이트 및 최신 트렌드의 코드,기술 반영 불가능


### AI 활용 방법

#### 1단계: 모델 선정

| 모델 | 장점 | 단점 | 선택 |
|------|------|------|------|
| GPT-4o | 빠른 속도 | 일관성 부족, 한국어 톤 부정확 | ❌ |
| **Claude Sonnet 4.5** | **한국어 자연스러움, 높은 일관성** | 비용 높음 | ✅ |
| Gemini 3 | 최신 LLM | 일관성 부족 | ❌ |

**선정 이유**
* "~해요", "~이에요" 같은 세밀한 한국어 톤 제어가 가능하고, JSON 스키마 준수율 95% 이상으로 안정적

#### 2단계: 프롬프트 엔지니어링 (반복 개선)

**개선 과정**
```
1차 시도 (60% 정확도) - 단순 지시형
"100자 이내로 친근하게 설명해줘" 
→ 추상적 지시어("친근하게", "간단하게")에 대한 AI의 해석이 제각각이었고, 여러 요구사항이 충돌할 때 우선순위가 불명확했습니다.

2차 시도 (80% 정확도) - 구조화된 지시 + 예시 제공
→정량적 기준(글자 수, 구조)은 잘 지켰지만, 정성적 기준(톤, 느낌)은 여전히 일관성 부족

3차 시도 (95~99% 정확도) - 계층적 프롬프트 시스템
→ [Base Prompt] - 역할과 원칙 정의
→ [Type Prompt] - 콘텐츠 유형별 템플릿
→ [강조 지시문] - 최종 품질 체크리스트
```

### 개선 결과

| 지표 | Before (수동) | After (AI) | 개선률 |
|------|--------------|-----------|--------|
| **생산성** |||
| 1개 생성 시간 | 10분 | 6초 | **99.0%** ↓ |
| 전체 소요 시간 | 2,067시간 | 20시간 | **99.0%** ↓ |
| 2인 팀 작업 기간 | 260일 | 3일 | **98.8%** ↓ |
| **비용** |||
| 총 비용 | 1억(사람 고용 시) | - | **99.0%** ↓ |
| **품질** |||
| 톤앤매너 일관성 | 60% | 95% | **58%** ↑ |
| 형식 정확도 | 80% | 98% | **23%** ↑ |
| 태그 정확도 | 50% | 100% | **50%** ↑ |

---

## ② 실제 사용한 프롬프트 템플릿

### 프롬프트 구조

```
Base Prompt (공통 규칙, 2,000 토큰)
+ Type Prompt (타입별 규칙, 500 토큰)  
+ 강조 지시문 (절대 규칙, 300 토큰)
```

### A. Base Prompt (핵심만 발췌)
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

### B.Type-specific Prompt 예시 (code_tip의 경우)

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
### C. 강조 지시문 예시
```markdown
## ⚠️ 강조 지시문 (출력 전 필수 체크리스트)

### 📋 출력 직전 반드시 확인할 것

**1. JSON 형식 검증**
✓ 유효한 JSON 구조인가? (중괄호, 쉼표, 따옴표 확인)
✓ 모든 필수 필드가 존재하는가? (type, title, description, tags 등)
✓ 문자열에 이스케이프되지 않은 특수문자 없는가?

**2. 글자 수 정확 카운트** (공백, 이모지 포함)
✓ title: 정확히 18자 이내 (17자가 최선)
✓ description: 40~50자 범위 (45자 목표)
✓ code: 각 줄이 40자 이내 + \\n으로 줄바꿈 표시

**3. 태그 규칙 준수** (가장 중요!)
✓ tags 배열에 1~2개만 포함되었는가?
✓ 공통 카테고리(algorithm, datastructure, os, network, databasetheory) 사용 시:
  → 반드시 단독 사용! 다른 태그와 조합 절대 금지!
  → 예: ["algorithm"] ✅  ["algorithm", "javascript"] ❌

**4. 타입별 톤앤매너**
✓ code_tip: "~해요", "~이에요" (친근한 존댓말)
✓ interview: "~입니다", "~합니다" (격식 있는 존댓말)
✓ code_review: "~하면 좋아요", "~추천해요" (조언하는 톤)
✓ 반말, 명령형 종결어("~해", "~하자") 절대 사용 금지

**5. 코드 품질**
✓ 코드에 주석 포함하지 않았는가? (주석은 description에)
✓ 줄바꿈이 \n이 아닌 \\n으로 이스케이프되었는가?
✓ 실행 가능한 코드인가? (문법 오류 없음)

**6. 언어 일관성**
✓ language 필드와 code의 실제 언어가 일치하는가?
✓ 혼용 금지: JavaScript 코드에 Python 문법 섞이지 않았는가?

### 🚫 절대 금지 사항
- "쉽게 말하면", "간단히", "대충" 같은 메타 표현
- 이모지 중복 (title에 1개만 허용)
- 코드와 무관한 설명 (예: "이 코드는 ~를 구현한 것입니다")
- 추상적 표현 ("적당히", "필요에 따라")

### ✅ 최종 확인
위 6개 항목을 모두 통과했다면 출력하세요.
하나라도 미흡하면 수정 후 재검증하세요.
```

**사용법:**
```
[Base Prompt]
+
[Type Prompt]
+
[강조 지시문]  ← 이 순서로 프롬프트 결합
```

### 프롬프트 개선 과정 (초안 → 최종)

**초안 (1차, 정확도 60%)**
```markdown
JavaScript 코드 팁 10개를 JSON으로 만들어줘
```
주요 문제점
* 추상적 지시어("친근하게", "간단하게")에 대한 AI 해석이 제각각이고 형식/길이/톤을 동시에 무시하는 케이스가 70% 발생했습니다.

---

**개선 1차 (2차, 정확도 80%)**
```markdown
다음 JSON 형식으로 JavaScript code_tip 10개 생성:
- title: 18자 이내
- description: 40-50자
- tags: javascript, typescript 등에서 선택

예시 3개 포함
```
개선 사항
* 100개 샘플 분석으로 실패 패턴을 찾아내고, 성공 예시 3개 + 구조화된 형식(제목 20자/본문 80자/요약 15자)을 명시했습니다.
  
남은 문제
* 정량적 기준(글자 수, 구조)은 잘 지켰지만 톤앤매너 같은 정성적 요소에서 여전히 15%정도 불일치했습니다.

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
개선 사항
* B**ase(역할 정의) → Type(콘텐츠 유형별 템플릿) → 강조(체크리스트) 3단계 계층**으로 우선순위를 자동 정립하고, AI가 출력 전 자가 검증하도록 설계했습니다.

### 생성 후에는? -> 3단계 품질 관리 시스템으로 검증!
```
1️⃣ 자동 검증 (100% 검사)
   ✅ JSON Schema, 길이, 태그 규칙등의 필수 요건을 다시한번 프롬프트를 통해 검증
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

* **기간**: 2025.07 ~ 진행 중
* **팀**: 1인 개발

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

### AI 활용 전략 
### **Claude Opus 4.5로 아키텍처 설계**

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
#### 결과
* <img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/5e92f1cc-79a0-4992-a48b-5798acf28a85" />
* **Claude 제안**: 모노레포, 멀티레포, 하이브리드 3가지 안 제시  
* **최종 선택** -> 멀티레포
*  **효과**: 아키텍처 설계 4시간 → 30분으로 단축

### **React <->Unity** 간 통신 프로토콜 설계
```
[프롬프트] 
React WebApp에 Unity WebGL을 임베드하고 양방향 통신하는 시스템을 설계해줘. 
보안, 성능, 확장성 측면에서 트레이드오프 분석 포함.
```
**생성 결과**
* <img width="500" height="450" alt="image" src="https://github.com/user-attachments/assets/173608ae-7308-4ac4-9ef1-19b28cb20b19" />
* **3-2 . RGF↔ React 통신 인터페이스 명세서**
	* https://yellow-candle-643.notion.site/3-2-RGF-React-2e6fbe9c2f9b806795bef3f8af4cf743?source=copy_link


### **Meshy.ai로 3D 에셋 자동 생성**
```
[프롬프트]
Create a 3D model of a vintage trolley train 
for a moral dilemma game. Low poly style.
```
**생성 결과**:
- 트롤리 기차 모델: 정점 500개, 폴리곤 300개
- 텍스처: 512x512
- 소요 시간: **5분** (직접 모델링 시 2주 예상)

### **멀티 플랫폼 채팅 통합 라이브러리 제작 (Gemini로 API 문서 분석)**

스트리머들이 플랫폼 선택 고민으로 멀티 스트리밍을 하면서 발생하는 채팅 분산 문제를 해결하기 위해 만들었습니다.  

각 플랫폼마다 채팅 API 방식이 다르고,제약이 다르기 때문에, 하나하나 구현하기에도 무리가 있다고 판단해서,모든 플랫폼 채팅을 **하나의 통일된 방식으로 받을 수 있는 어댑터 라이브러리를 제작**했습니다.

```markdown
[프롬프트 to Gemini]
다음 3개 플랫폼의 채팅 API 비교:
1. Chzzk Chat API [문서 URL]
2. YouTube Live Chat API [문서 URL]  
3. Soop(아프리카TV) 채팅 API [문서 URL]

공통점과 차이점을 표로 정리하고,
TypeScript 어댑터 인터페이스 제안해줘.
```
**Gemini 분석 결과** (처리 시간: 1시간 → 10분)

| 플랫폼 | 연결 방식 | 메시지 형식 | 인증 |
|--------|----------|------------|------|
| CHZZK| WebSocket | JSON | OAuth |
| YouTube | HTTP Polling | JSON | API Key |
| SOOP(아프리카TV) | WebSocket | JSON | Session |

![501994260-0ac6b384-47d3-4059-a618-0bba199ecee7](https://github.com/user-attachments/assets/1a80be14-c2ea-4f4b-9232-85ab7c79e2ae)


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

### AI별 기여도

| AI 도구 | 사용 시간 | 주요 용도 |
|---------|----------|---------------|
| Claude Opus 4.5 | 2시간 | 아키텍처 |
| Claude Code | 8시간 | 핵심 로직(React <->Unity** 간 통신 프로토콜) 구현|
| Meshy.ai | 1시간  | 3D 에셋 |
| Gemini | 3시간  | API 문서 분석 및 인터페이스 생성 |
| **합계** | **14시간**  | - |

### 성과 및 개발 시간 분석

 AI 효과 분석
   - AI 미사용 시 예상: 420시간
   - 실제 소요: 68시간
   - 절감률: 83.8% (352시간 절약)
   
주요 절약 항목:
- 3D 에셋 생성: 335h (AI 이미지 생성)
- API 통합: 7h (문서 자동 분석)
- 보일러플레이트: 8h (코드 자동 생성)
- 아키텍처 설계: 3.5h (구조 제안)

---

# 프로젝트 C: ifland (메타버스 플랫폼)
> ⚠️ **주의**: 본 섹션은 개인 업무 효율화 사례입니다. 회사 공식 AI 도입 사례가 아닙니다.

SK텔레콤의 소셜 메타버스 플랫폼 **ifland** 클라이언트 개발에 참여했습니다. 사용자가 아바타를 커스터마이징하고 가상 공간에서 파티, 세미나, 공연 등 다양한 활동을 즐길 수 있으며, NFT 기반 아이템과 후원 기능 등 경제 시스템을 갖춘 플랫폼입니다.
* **기간**: 2022.06 ~ 2024.10 (2년 5개월)
* **팀**: 클라이언트 개발팀

### 역할 및 기여도

| 영역 | AI 활용 (개인) |
|------|-----------|
| Unity 클라이언트 개발 | ChatGPT |
| 볼류메트릭 콘서트 | **ChatGPT  (로그 분석)** |
| AI 페르소나 NPC개발 |**ChatGPT (API 분석)** |
| 성능 최적화 | ChatGPT |

### 기술 스택
- **Game Engine**: Unity, C#
- **External**: Microsoft MRCS (Volumetric Video), AI Persona Engine
- **AI Tools**: ChatGPT, Claude (개인 업무 효율화)

### 성과
- 누적 다운로드 **870만 건**
- 제휴 요청 **2,000건 이상**
- 최대 **131명 동시 참여** 지원
---

## 사례 : 환각(Hallucination) - 존재하지 않는 API 제안
<img width="1280" height="606" alt="image" src="https://github.com/user-attachments/assets/e42e1247-ce59-4f48-9657-692d6e89cdb5" />

배경 

- 볼류메트릭 콘서트 기능 개발 중 Microsoft MRCS 통합 과정에서 알 수 없는 에러 발생. 50줄 이상의 스택 트레이스로 원인 파악이 어려운 상황.

```markdown
csharp[ERROR] MRCSStreamingException: Failed to initialize volumetric stream
at Microsoft.MixedReality.Streaming.VolumetricStreamManager.Initialize()
at IflandMetaverse.Features.Concert.VolumetricConcertController.StartStream()
... (50줄 이상)
```

ChatGPT 활용 및 문제점

```markdown
[프롬프트]
다음 에러 로그를 분석해줘. Microsoft MRCS Unity SDK 사용 중.
[에러 로그 전체]
```

ChatGPT 응답
```markdown
MRCSConfig.EnableAutoRetry()를 true로 설정하면
연결 실패 시 자동 재시도됩니다.
```

**환각 발견**
-  `MRCSConfig.EnableAutoRetry()` → ❌!!!**공식 문서에 존재하지 않는 API**

**해결 방법으로 검증 시스템 도입**

1. AI에게 질문 (개선된 프롬프트)
   - SDK 버전 명시
   - 공식 문서 URL 요구
   - 검색 허용

2. 수동 검증
   - 공식 문서 크로스 체크
   - Unity Forum/GitHub Issues 검색
   - 실제 DLL 메타데이터 확인

개선된 프롬프트
```
Microsoft MRCS Unity SDK 1.2.3 기준으로 에러 해결 방법 알려줘:
[에러 로그]

⚠️ 제약사항:
- 공식 문서에 명시된 API만 사용
	[공식 링크 첨부]
- 각 방법마다 공식 문서 URL 첨부

출력 형식:
1. 방법: [정확한 API/설정]
2. 문서 근거: [URL]
3. 주의사항: [있다면]
```

**결과**
* 환각 발생률: 30% → 0%
* 에러 분석 시간: 3시간 → 20분 (90% 단축)
