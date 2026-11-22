# AI 리터러시 학습 진행 기록

2026년 11월 22일 기준. [워밍업에서 설명한 여섯 개념](ai-learning-context.md)을 출발점으로, 모델이 학습하는 방식에서 주문 앱의 실행 흐름까지 살펴봤다.

## 다룬 질문

| 질문 | 대화에서 정리한 내용 |
| --- | --- |
| 생성형 AI, LLM, AGI는 어떤 관계인가? | 생성형은 출력의 성격, LLM은 모델 계열과 규모, AGI는 능력의 범위와 수준을 가리킨다. 강한 AI의 철학적 원뜻은 컴퓨터에 실제 이해를 귀속할 수 있는가에 관한 입장이다. [AGI 연구](https://deepmind.google/research/publications/66938/) · [강한 AI 원문](https://www.cs.tufts.edu/comp/50cog/readings/searle.html) |
| LLM에서 딥러닝은 어디에 해당하는가? | 트랜스포머는 계산 구조이고, 딥러닝은 여러 층의 신경망에서 데이터의 패턴을 학습하는 접근이다. 학습에서는 가중치를 조정하고 추론에서는 학습한 가중치로 새 입력의 결과를 계산한다. [Google의 LLM 설명](https://developers.google.com/machine-learning/crash-course/llm/transformers) |
| 규모가 비슷한 전용 모델은 무엇이 다른가? | 약 3억 파라미터인 OPT-350M, ViT-Large, wav2vec 2.0 LARGE를 비교했다. 언어·비전·음성 모델이 비슷한 구조를 써도 입력과 학습 목표에 따라 수행하는 일이 달라진다. 앱이 음성을 받는다면 원본 녹음을 처리하는 모델과 전사된 글을 요약하는 모델을 각각 확인한다. [OPT](https://arxiv.org/pdf/2205.01068) · [ViT](https://arxiv.org/html/2010.11929) · [wav2vec 2.0](https://arxiv.org/abs/2006.11477) |
| MCP에서 스킬과 도구는 어떻게 다른가? | 스킬은 에이전트가 읽는 업무 지침과 보조 파일이다. 도구는 서버가 이름과 입력 형식으로 공개한 호출 가능한 기능이다. 클라이언트는 `tools/list`로 목록을 조회하고 `tools/call`로 도구를 실행한다. [도구 명세](https://modelcontextprotocol.io/specification/2026-07-28/server/tools) · [Agent Skills](https://agentskills.io/what-are-skills) |
| 에이전트와 MCP 호스트의 역할은 무엇인가? | 호스트는 클라이언트를 관리하는 앱이다. 에이전트는 목표와 중간 결과를 바탕으로 다음 행동을 선택한다. 호스트가 에이전트 실행을 담당할 수도 있고, 버튼이 정해진 도구만 호출하는 앱도 호스트가 될 수 있다. [MCP 아키텍처](https://modelcontextprotocol.io/specification/2026-07-28/architecture) · [에이전트와 워크플로](https://www.anthropic.com/research/building-effective-agents) |

## 마지막으로 살펴본 사례 — Spring 주문 앱

버튼 주문과 채팅 주문이 같은 주문 서비스를 사용할 수 있다. 버튼 경로에서는 컨트롤러가 주문 서비스를 호출한다. 채팅 경로에서는 에이전트가 주문 스킬을 참고해 옵션을 더 물을지, 주문 도구를 호출할지 결정한다. MCP 클라이언트가 호출을 전달하면 서버 측 도구가 주문 서비스를 이용한다. 두 경로 모두 재고·권한 검증과 저장은 주문을 처리하는 시스템이 담당하며, 성공의 근거는 그 시스템이 반환한 주문 결과다. [Spring MVC의 요청 처리](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet.html)

## 다음에 확인할 실무 이해

사용자가 새 사례에 위 구분을 적용해 설명하는 단계가 남아 있다. 배송지 변경을 예로 들어, 어느 구성요소가 추가 정보를 묻고, 어디서 변경 권한을 검증하며, 어떤 결과를 받아야 고객에게 변경 완료를 알릴 수 있는지 따라가 본다. 사용자가 직접 표시한 항목과 횟수는 [개념 체크리스트](../개념%20체크리스트.md)에 기록한다.
