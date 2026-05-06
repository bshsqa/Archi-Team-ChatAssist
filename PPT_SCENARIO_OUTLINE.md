# SPRAG 기반 사내 메신저 AI Assistant PPT 시나리오

## 문서 목적

본 문서는 `SPRAG 기반 사내 메신저 AI Assistant` 과제를 5장 이내의 PPT로 정리하기 위한 페이지별 구성안이다. 실제 발표에서는 SPRAG 알고리즘 자체를 상세히 설명하기보다, SPRAG을 사용하는 Offline/Online Pipeline을 왜 설계해야 하는지와 그로 인해 어떤 품질속성을 만족하는지를 중심으로 설명한다.

## 전체 발표 메시지

> 우리는 AI Chatbot 자체를 만드는 것이 아니라, 중복 많은 사내 지식과 다중 세션 맥락을 안전하고 저비용으로 LLM에 공급하는 SPRAG Pipeline Architecture를 설계한다.

## Slide 1. Problem and Background

### 핵심 메시지

사내 업무 지식은 여러 시스템에 흩어져 있고 중복이 많아, 기존 RAG 방식만으로는 정확성, 비용, 보안 요구를 동시에 만족하기 어렵다.

### 포함 항목

- 사내 지식의 파편화
  - 메신저 대화
  - Confluence/Wiki 문서
  - Jira 티켓
  - 회의록 및 장애 기록
- 기존 검색/RAG의 한계
  - 유사 문서와 버전 중복
  - 불필요한 Vector 저장 및 LLM 입력 토큰 증가
  - 오래된 정보와 최신 정보의 충돌
  - 사용자가 매번 업무 맥락을 다시 설명해야 하는 불편
- 아키텍처 문제 정의
  - 중복 많은 원본 데이터에서 적은 토큰으로 정확한 근거를 추출해야 한다.
  - Multi-turn, Multi-session 질문을 지원해야 한다.
  - 권한 없는 정보가 LLM 컨텍스트에 포함되면 안 된다.

### 발표 메모

이 슬라이드에서는 "왜 단순 Chatbot이 아니라 RAG Pipeline 설계가 필요한가"를 설명한다. 특히 중복 데이터와 다중 세션 맥락을 문제의 중심에 둔다.

## Slide 2. Target Service and Stakeholders

### 핵심 메시지

목표 서비스는 사내 메신저에 통합된 AI Assistant이며, 사용 편의성뿐 아니라 비용, 보안, 운영, 유지보수 요구를 함께 만족해야 한다.

### 포함 항목

- 목표 서비스
  - 사내 메신저에서 사용자의 현재 대화 맥락을 파악한다.
  - 접근 가능한 과거 대화 세션과 사내 문서를 검색한다.
  - 출처 기반으로 신뢰 가능한 답변을 제공한다.
- 주요 Stakeholder
  - 일반 임직원: 정확하고 빠른 답변
  - 팀 리더: 과거 의사결정과 업무 맥락 재활용
  - 경영진/스폰서: LLM 비용 대비 생산성 향상
  - 보안/컴플라이언스 담당자: 권한 및 보존 정책 준수
  - 시스템 운영자: 안정성, 확장성, 장애 대응
  - 지식 관리자: 중복 문서와 오래된 문서 관리
- Stakeholder별 대표 품질속성
  - Functional Suitability
  - Performance Efficiency
  - Security
  - Reliability
  - Maintainability

### 발표 메모

이 슬라이드에서는 AI 기능을 원하는 사용자만이 이해관계자가 아니라는 점을 강조한다. 특히 보안 담당자와 운영자의 요구가 아키텍처 결정에 큰 영향을 준다.

## Slide 3. Key Use Cases

### 핵심 메시지

Use Case는 단순 질의응답보다, SPRAG Pipeline과 Multi-session Context가 필요한 상황을 중심으로 구성한다.

### 포함 항목

| Use Case | 설명 | 설계 포인트 |
| --- | --- | --- |
| 멀티 세션 업무 회고 | 과거 여러 대화방과 문서를 묶어 프로젝트 이력을 요약 | 세션 검색, 권한, 컨텍스트 조립 |
| 사내 문서 질의응답 | 최신 정책, 기술 문서, Jira 이슈를 근거로 답변 | SPRAG 중복 제거, 출처 신뢰도 |
| 그룹 채팅 지원 | 참여자들이 접근 가능한 정보만 사용해 논의 보조 | ACL 교집합, 정보 노출 방지 |
| 세션 참조 제어 | 특정 대화방을 AI 참조 대상에서 제외 | Opt-in/out, 정책 동기화 |
| 충돌 정보 판별 | 공식 문서와 대화 내용이 다를 때 출처와 기준 제시 | 최신성, Authority, Conflict Resolution |

### 발표 메모

Use Case를 너무 많이 나열하기보다, 아키텍처 품질속성과 연결되는 대표 Use Case만 보여준다. 스마트 링크 자동 제공은 시간이 남을 때 보조 기능으로 언급한다.

## Slide 4. Functional Scope and Pipeline

### 핵심 메시지

아키텍처는 Offline SPRAG Pipeline과 Online Retrieval Pipeline으로 나누어 설계한다.

### 포함 항목

#### Offline SPRAG Pipeline

1. 원본 데이터 수집
2. 정규화 및 민감정보 마스킹
3. 중복/유사 데이터 탐지
4. 대표 청크 또는 압축 표현 생성
5. 권한, 출처, 버전, 최신성 메타데이터 부여
6. Vector DB 및 Metadata Store 인덱싱

#### Online Retrieval Pipeline

1. 사용자 질의 및 현재 세션 맥락 수신
2. 사용자/그룹 권한 정책 계산
3. Vector Search 및 Metadata Filtering
4. Re-ranking 및 Top-K 선정
5. 출처 신뢰도와 최신성 기반 컨텍스트 조립
6. LLM 답변 생성 및 출처 표시

### 발표 메모

이 슬라이드는 과제의 중심이다. SPRAG 내부 알고리즘은 블랙박스로 두되, Offline 단계에서 어떤 책임을 수행하고 Online 단계에서 어떤 정책을 적용하는지 명확히 나누어 설명한다.

## Slide 5. Quality Attributes and Architecture Drivers

### 핵심 메시지

본 아키텍처의 주요 설계 결정은 ISO/IEC 25010 품질속성 중 Functional Suitability, Performance Efficiency, Security, Reliability, Maintainability에 의해 주도된다.

### 포함 항목

| ISO/IEC 25010 품질특성 | Architecture Driver | 설계 대응 |
| --- | --- | --- |
| Functional Suitability | 정확한 근거 선택 | Re-ranking, Top-K, 출처 기반 답변 |
| Performance Efficiency | 토큰 비용과 응답시간 절감 | SPRAG 중복 제거, 컨텍스트 압축, 캐싱 |
| Security | 권한 없는 정보 차단 | ACL Metadata Filtering, Opt-in/out |
| Reliability | 일부 시스템 장애에도 서비스 유지 | Offline/Online 분리, 재처리, 저하 모드 |
| Maintainability | 정책 변경 용이성 | 검색 가중치, Top-K, TTL, 출처 우선순위 설정화 |
| Portability | 기술 요소 교체 가능성 | Vector DB, LLM Provider, Embedding 모델 추상화 |

### 발표 메모

마지막 슬라이드에서는 요구사항 목록을 반복하기보다, 품질속성이 실제 아키텍처 구조를 어떻게 결정했는지 연결한다. 예를 들어 보안성은 ACL 필터링을 만들고, 성능 효율성은 Offline SPRAG과 Top-K 제한을 만든다는 식으로 설명한다.

## PPT 작성 팁

- 5장 안에서는 서비스 기능보다 Architecture Driver를 우선한다.
- SPRAG 기술 자체는 블랙박스로 두고, 입력/출력/책임을 명확히 표현한다.
- `Cost`, `Latency`, `Scalability`는 발표 중에는 직관적으로 말해도 되지만, 문서 표기는 ISO/IEC 25010 기준으로 정리한다.
- 그림을 넣는다면 Slide 4에 Offline/Online Pipeline 한 장을 넣는 것이 가장 효과적이다.
- 결론 문장은 "SPRAG은 중복 제거 기술이 아니라, 사내 지식을 LLM에 안전하고 효율적으로 공급하기 위한 Pipeline Architecture의 핵심 구성요소"로 잡으면 좋다.
