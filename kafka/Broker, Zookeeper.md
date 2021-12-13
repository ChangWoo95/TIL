#Broker, Zookeeper

##Broker란?
### Topic과 Partition을 유지 및 관리해주는 소프트웨어
- partition에 대한 Read 및 Writer를 관리힘
- Topic 내의 Partition들을 분산, 유지 및 관리해줌
- Kafka Server라고 부르기도 함
- 각각의 Broker들은 ID로 식별된다(ID는 숫자)
- Topic의 일부 Partition들을 포함함
- 특정 Broker에 연결하면 전체 클러스터에 연결됨
- 최소 3대 이상의 Broker를 하나의 Cluster로 구성해야함(보통 4대 이상을 권장함)
- Topic을 구성하는 Partition들은 여러 Broker 상에 분산됨
- 모든 Kafka Broker는 Bootstrap 서버라고 부름

##Zookeeper란?
### Kafka의 Broker를 관리해주는 소프트웨어
- 변경사항에 대해 Kafka의 모든 Broker에 알림(ex. Topic 생성/제거, Broker 추가/제거 등)
- Zookeeper없이는 Kafka가 작동할 수 없음(KIP-500을 통해 Zookeeper 제거가 진행 중임)
- 홀수의 서버로 작동하게 설계되어 있음(최소 3, 권장 5)
- Leader와 Follower의 개념의 구조
- 분산 작업을 제어하기 위한 Tree 형태의 데이터 저장소가 있음
- Quorum 알고리즘(정족수, 과반수 이상이 남아 있다면 정상동작)으로 구현되어 있음




