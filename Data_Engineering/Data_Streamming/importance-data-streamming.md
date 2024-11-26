## 실시간 데이터 처리의 중요성

> 🤔 실시간 처리가 왜 중요해졌을까? 구체적인 사례가 있을까?

- 실시간 처리의 중요성
  - 배치 처리는 일정 기간마다 모인 데이터를 벌크형으로(한꺼번에) 처리하기 때문에 어느 정도 데이터 쌓인 후 결과를 얻어내는 월별 분석 리포트, 대시보드 등에 활용
  - 실시간으로 현황을 보거나 서비스를 활용하는 상황에서는 **배치 처리**는 도움이 되지 못할 수도 있음.(미니 배치라는 개념도 있기에 `못할 수도 있다` 라고 표현)

- 구체적인 사례
  - 실시간 시내버스 및 지하철 현황표
  - 스트리밍 생방송 플랫폼
  - 채팅 시스템

> 🤔 버스 현황 서비스나 채팅 서비스 같은 실시간 데이터의 경우, 단순히 실시간 처리만 되는 것으로 충분할까?  
> 예를 들어, 버스 위치 데이터가 실시간으로 제공되지만 데이터가 손실되거나 정확하지 않다면 사용자에게 어떤 문제가 생길까? 

- 데이터가 손실되거나 정확하지 않은 채로 서비스에 나오게 된다면 데이터 품질이 낮아지고 잘못된 정보를 기반으로 의사 결정을 내릴 수 있음
  - *A-1번 버스를 타는 곳은 A아파트 앞이라고 표시되어 있는데, 알고보니 B아파트 앞에서 탑승*
  - *현재 여름이고 어제까지만 해도 무더위가 지속되었는데, 내일 일기예보는 눈이 올 것이라고 예측*

> 실시간 데이터 손실 또는 신뢰성 문제를 해결하기 위해 데이터 파이프라인은 어떤 역할을 해야 할까?

- 데이터 복제 또는 스트리밍 플랫폼
  - 데이터를 여러 장소에 복제하거나 메세징 큐(Kafka, RabbitMQ)를 통해 데이터를 손실없이 전달
- 체크포인팅
  - 데이터 처리가 중간에 실패되더라도 이전 상태로 복구할 수 있도록 상태를 주기적으로 저장
- 이벤트 순서 보장
  - 실시간 데이터의 순서를 보장하지 않은채로 처리 후 저장된다면 잘못된 결과가 나올 수 있음. 순서 보장 알고리즘(Kafka's Offset)을 사용
- 데이터 검증
  - 데이터 품질을 체크하고 오류 데이터는 별도로 기록
- 이중 파이프라인 구성
  - 실시간으로 처리되는 저장소 이외에 파일 기반 또는 배치 처리로 데이터 안정성을 확보

참고: [실시간 데이터 품질 관리와 이상 감지: 2024년 한국의 현황과 미래 전망](https://npf.kr/%EC%8B%A4%EC%8B%9C%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%92%88%EC%A7%88-%EA%B4%80%EB%A6%AC%EC%99%80-%EC%9D%B4%EC%83%81-%EA%B0%90%EC%A7%80-2024%EB%85%84-%ED%95%9C%EA%B5%AD%EC%9D%98-%ED%98%84/)

---


> 🤔 Deep Dive Question

1. [실시간 데이터 처리 중 데이터 순서가 뒤바뀌는 문제가 생겼다면 어떤 결과가 발생할 수 있을까? 이를 해결하는 방법은 무엇일까?](./data-ordering-issues-and-solutions.md)
