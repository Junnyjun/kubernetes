##### 새로운 인프라 환경이 온다. 

온프레미스 인프라 환경-> 필요에 따라 조합하고 선택하여 사용할 수 있는 서비스로써의 인프라 환경

> 컨테이너 인프라 환경 

하나의 운영체제 커널에서 다른 프로세스에 영향을 받지 않는 독립적으로 실행되는 프로세스 

######  :-1:모눌리식 아키텍쳐

하나의 큰 목적이 있는 서비스 또는 어플리에키엿ㄴ에 여러기능이 통합되어 있는 구조.

! 개발이 단순하며 코드관리가 용이 

###### :+1: MAS 아키텍쳐

개별 기능을 하는 작은 서비스를 각각 개발해서 연결하는 차이가 있다.

보안 인증 등 기능이 독립된서비스를 구성하고 있으며 다른서비스들도 독립적으로 동작할 수 있는 구조



> 컨테이너 인프라 환경을 지원하는 도구



- ###### Docker

컨테이너 환경에서 독립적으로 어플리케이션으 ㄹ실행할 수 있도록 컨테이너를 만들고 관리

- ###### Kubernetes

다수의 컨테이너를 관리하는 데 사용.

컨테이너의 자동 배포와 배포된 컨테이너에 동작 보증, 부하에 따른 동적 확장등을 제공

- Jenkins 

지속적 통합 (CI) & 지속적 배포 (CD) 를 지원한다.

빌드 테스트 패키지화 배포를 모두 자동화해 개발단계를 표준화

- Prometheus & Grafana

모니터링을 위한 도구 프로메테우스는 상태 데이터를 수집 그라파나는 수집한 데이터를 시각화 한다.
