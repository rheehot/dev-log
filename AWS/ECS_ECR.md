## AWS ECS & ECR

<br>

### :book: AWS ECS

> 컨테이너를 적절하게 배치하고 관리할 수 있게 도와주는 오케스트레이션 서비스이다.

<br>

`클러스터(Cluster)`

- 도커 컨테이너를 실행할 수 있는 가상의 공간으로 이해할 수 있다.

- 기본적으로 EC2와 같은 컴퓨팅 자원을 기본적으로 포함하고 있지 않은 논리적인 단위이다.

<br>

`컨테이너 인스턴스(Container Instance)`

- 클러스터에 연결된 EC2 인스턴스를 보통 컨테이너 인스턴스라고 부른다.

<br>

`태스크(Task)`

- 컨테이너를 실행하는 최소 단위이다.

- 태스크는 하나 이상의 컨테이너로 구성된다. (일반적으로 하나의 필수 컨테이너만으로 구성됨)

- 필요에 따라 하나의 필수 컨테이너와 n개의 추가적인 컨테이너의 조합이 될 수 도 있다.

- 같은 태스크로 실행되는 컨테이너들은 모두 같은 컨테이너 인스턴스에서 실행되는 것이 보장된다.

<br>

`태스크 데피니션(Task Definition)`

- 태스크를 실행하기 위해 필요한 설정들을 하나의 단위로 정의한 것이라고 이해하면 된다.

- 네트워크 모드, 태스크의 역할, 도커 이미지, 실행 명령어, CPU 제한, 메모리 제한 등 다수의 설정이 필요하다.

<br>

`서비스(Service)`

- 서비스를 정의해서 태스크를 실행할 수 있다.

- 서비스는 하나의 태스크 데피니션(리비전)과 연결된다.

- 서비스는 데몬 타입과 리플리카 타입이 있다.

  `데몬 타입`

  - 모든 컨테이너 인스턴스에 해당하는 태스크가 하나씩 실행된다.

  - 인스턴스 관리를 위한 용도로 많이 사용된다.

  `리플리카 타입`

  - 실행하려는 태스크의 개수를 지정해야한다.

  - 서비스는 클러스터에서 개수만큼 태스크가 실행되도록 자동적으로 관리해준다.

  - 웹서버를 비롯한 실제 서비스에서 주로 사용된다.

- 어떤 프로세스를 언제 배치할지 결정할 필요없이 오케스트레이션에서는 이러한 관리를 담당하는 스케줄러가 존재한다.

- ECS에서는 서비스가 이러한 스케줄링을 담당하고 있다.

- 각 인스턴스들에 설치된 esc-client에서 수집된 정보를 기반으로 태스크를 언제 실행할지 결정한다.

<br>

### :book: AWS ECR

> 프라이빗 도커 레지스트리 서비스를 제공한다. 도커 레지스트리는 도커 이미지를 저장하고 관리하는 서비스이다.

<br>

### :bookmark: 참고

- [https://www.44bits.io/ko/post/container-orchestration-101-with-docker-and-aws-elastic-container-service](https://www.44bits.io/ko/post/container-orchestration-101-with-docker-and-aws-elastic-container-service)
