# Apache Kafka 주요 요소

## Topic
### Kafka 내에서 메세지가 저장되는 장소
- 논리적인 표현으로서, 시스템 상에서 눈으로 보이지는 않음

## Producer
### 메세지를 생산(produce)해서 Kafka의 Topic으로 메세지를 보내는 애플리케이션

## Consumer
### Topic의 메세지를 가져와서 소비(Consume)하는 애플리케이션
- Consumer는 흔히 Consumer Group으로 관리가 됨

## Consumer Group
### Topic의 메세지를 사용하기 위해 협력하는 Consumer들의 집합
- 하나의 Consumer는 하나의 Consumer Group에 포함되며, Consumer Group 내의 Consumer들은 협력하여 Topic의 메세지를 분산 병렬 처리함
- 다른 Consumer Group에 속한 Consumer들은 서로 관련이 없으며, Commit Log에 있는 Event(Message)를 동시에 다른 위치에서 Read할 수 있음

## Producer와 Consumer의 분리(Decoupling)
### Producer와 Consumer의 기본 동작 방식
- Producer와 Consumer는 서로 알지 못하며, Producer와 Consumer는 각각 고유의 속도로 Commit Log에 Write 및 Read를 수행
<img src="https://user-images.githubusercontent.com/59639001/145717552-8a47da78-f300-4f0b-8ad4-71a333245cf7.png">

### Commit Log란?
- 추가만 가능하고 변경 불가능한 Data Structure
- 데이터(Event)는 항상 로그 끝에 추가되고 변경되지 않음
- **Offset**은 Commit Log에서 Event의 위치를 나타냄
- producer가 Commit Log에 마지막으로 Write하는 **LOG-END-OFFSET**과 Consumer Group의 Consumer가 Read하고 마킹(commit)하는 **CURRENT-OFFSET**과의 차이(**ConsumerLag**)가 발생할 수 있음

## Kafka의 Logical View
<img src="https://user-images.githubusercontent.com/59639001/145717910-97f54f41-c84c-4ae6-bc3d-da6223ad02ac.png">

### Partition
- Commit Log
- 하나의 Topic은 하나 이상의 Partition으로 구성함
- **병렬처리**를 위해 다수의 Partition을 사용함

### Segment
- 메세지(data)가 저장되는 실제 물리 File
- Segment File이 지정된 크기보다 크거나 지정된 기간보다 오래되면 새 파일이 열리고 메세지는 새 파일에 추가됨

## Kafka의 Physical View
<img src="https://user-images.githubusercontent.com/59639001/145718070-c89d18b0-5f6a-46e1-b8ff-68f5d63e28e1.png">

- Topic 생성 시, Partition 개수를 지정하고, 각 Partition은 Broker들에 분산되며 Segment File들로 구성됨

## Active Segment
<img src="https://user-images.githubusercontent.com/59639001/145718190-18e53010-db35-4d31-be12-750790fe3b36.png">

- Partition당 오직 하나의 Segment가 활성화(**Active**)되어 있음

<img src="https://user-images.githubusercontent.com/59639001/145718786-f65db962-aa14-434a-ada1-edc543d49139.png">
