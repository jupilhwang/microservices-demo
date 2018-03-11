

### Sock Shop : A Microservice Demo Application

1. Microservices demo
2. CQRS
3. Side-Car with Istio


이 응용 프로그램은 양말을 판매하는 온라인 상점의 사용자 인터페이스 부분입니다. Microservice 와 Cloud Native 기술 데모 및 테스트를 돕기위한 것으로, WeaveWorks에서 Open Source로 배포한 것입니다.
출처 : http://github.com/microservices-demo/microservices-demo

Spring Boot, Go Kit, Node.js on Docker env.

#### Screenshot
![](./img/sockshop-frontend.png)


### Design
#### 목표
- Demonstrate microservice best practices (and mistakes!)
- Be cross-platform: deploy to all orchestrators
- Show the benefits of continuous integration/deployment
- Demonstrate how dev-ops and microservices compliment each other
- Provide a "real-life" testable application for various orchestration platforms

#### Architecture
![](./img/Architecture.png)

microserivces 응용 프로그램의 아키텍처는 가능한 한 많은 마이크로 서비스를 제공하기 위해 의도적으로 설계되었습니다. 자신만의 디자인을 고려하고 있다면 반복적인 접근 방식을 권장합니다.이 방식을 사용하면 응용 프로그램에서 문제(성능 / 테스트 / 커플링)가 발생할 때 새로운 마이크로서비스 만 정의 할 수 있습니다.
또한, 여러 가지 기술을 연습하는 것은 의도적으로 Polyglot으로 구성되었습니다. 필요에 따라 신기술만 고려하면 됩니다.

위 이미지에서 알 수 있듯이 마이크로 서비스는 대략 전자 상거래 사이트의 기능에 의해 정의됩니다. 모든 서비스는 HTTP를 통한 REST를 사용하여 통신합니다. 이것은 개발 및 테스트의 단순성으로 인해 선택되었습니다. API는 개발 중입니다.
[출처:weaveworks microservices-demo]

