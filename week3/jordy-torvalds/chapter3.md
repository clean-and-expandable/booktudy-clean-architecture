# 3부.설계 원칙
SOLID 원칙은 함수와 데이터 구조를 클래스로 배치하는 방법, 그리고 이들 클래스를 서로 결합하는 방법을 설명해준다. SOLID 원칙의 목적은 중간 수준의 소프트웨어 구조가 아래와 같도록 만드는데 있다.

- 변경에 유연하다.
- 이해하기 쉽다.
- 많은 소프트웨어 시스템에 사용될 수 있는 컴포넌트의 기반이 된다.

중간 수준이라 함은 프로그래머가 이들 원칙을 모듈 수준에서 작업할 때 적용할 수 있다는 뜻이다.

# 7장. SRP: 단일 책임 원칙

하나의 모듈은 하나의, 오직 하나의 사용자 또는 이해관계자에 대해서만 책임져야 한다.

이해관계자는 해당 변경을 요청하는 한 명 이상의 사람들을 가리키며, 이러한 집단을 액터라고 한다.

책에서 예로 들은 Employee란 클래스는 이해관계자가 여럿 존재한다.  임금 계산이 필요한 회계팀, 근무 시간 현황 보고가 필요한 인사팀, 직원 정보 추가가 필요한 DBA 팀이 서로 다른 목적으로 해당 클래스에 기능 추가 및 개선을 요청한다.  Employee라는 클래스가 가진 책임이 하나가 아니고 여러 이해관계를 위한 기능을 갖춘 병합된 클래스가 되는 것이다. 이러한 클래스는 각각의 이해관계자를 위해 변경이 발생하다보면 버그를 만들어 낼 수 있으며 지양해야 한다. 그래서 병합된 클래스를 각 이해 관계를 위해 분리가 필요하다.

책에서는 세부적인 방안으로 퍼사드 패턴을 제안한다. 단일 책임 원칙은 메서드와 클래스 수준의 원칙인데 이보다 더 상위로 올라가 아키텍처 관점에서 바라보면 공통 폐쇄 원칙이란 개념으로 등장한다. 

공통 폐쇄 원칙은 동일한 이유로 동일한 시점에 변경되는 클래스를 같은 컴포넌트로 묶어라. 서로 다른 시점에 다른 이유로 변경되는 클래스는 다른 컴포넌트로 분리하라는 원칙이다. 이 원칙은 결합도를 낮추고, 응집도를 높이기 위한 원칙으로 보이며 세부 내용은 이후에 장에서 다룬다.

# 8장. OCP: 개방 폐쇄 원칙

소프트웨어 개체는 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다.

다시 말해 소프트웨어 개체의 행위는 확장할 수 있어야 하지만, 이때 변경이 발생해서는 안된다. 소프트웨어 아키텍처를 공부하는 이유도 바로 이 떄문이다. 만약 요구사항을 살짝 확장하는데 소프트웨어를 엄청나게 수정해야 한다면, 그 소프트웨어 시스템을 설계한 아키텍트는 엄청난 실패를 맞닥뜨린 것이다.

![image](https://user-images.githubusercontent.com/58139899/147716200-01f4998b-6e58-41ea-a14f-3586628f403e.png)

재무 데이터를 분석해서 만들어진 보고서용 재무데이터를 목적에 따라 웹에 표시하거나 프린터로 출력할 수 있을 것이다. 이 두 가지 출력 방식은 앞선 장에서 공부했듯이 서로 다른 책임을 가지고 있기 때문에 분리 되어야 하고 변경 발생시 상호간에 영향을 주지 않아야 한다. 

OCP는 보고서용 재무데이터를 표현 하는 방식이 더 추가된다고 했을 때 기존 코드에 변경 없이 표현방식이 확장될 수 있어야 함을 강조하는 원칙이다.

![image](https://user-images.githubusercontent.com/58139899/147716211-9b9a9752-cac4-4145-80a9-5771e2b0650c.png)
- 'I'는 인터페이스 이고 'DS'는 데이터 구조를 표현한다.
- 열린 화살표는 사용 관계를 의미한다.
- 닫힌 화살표이면서 색칠이 되어 있지 않으면 구현 관계이고, 색칠이 되어 있으면 상속 관계이다.

클래스 다이어그램을 보면 알 수 있는 점은 클래스가 추상적인 인터페이스에 의존하고 있고, 실제 구현체는 구현 관계에 있음을 알 수 있다. 컴파일 타임에서의 의존 관계와 런타임 시점에서의 의존관계가 달라지게 되는 셈이다.

또한 클래스간 양방향 관계가 없으며 인터페이스를 사용해 의존관계를 역전시키고 있음을 알 수 있다. 또한 이를 통해 변경이 발생했을 때 영향도가 전파되는 것을 막으면서, 캡슐화를 통해 세부 구현에 다시 알지 않아도 되게 한다.

**변경이란?**
특정 인터페이스를 구현한 클래스라고 가정하고 변경에는 어떤 것이 있고 DIP를 했을 때 클라이언트 클래스에 영향을 주는지를 여부를 판단해보자.(컴파일 에러를 발생 시키는지 여부)

- 클래스명을 변경하는 상황
→ X
- 다른 구현체로 대체되어야 하는 상황
→ X
- 인스턴스/스태틱 메소드/변수/상수를 추가하는 상황
→ X
- 인터페이스로부터 오버라이드 중인 메소드의 이름을 변경하는 경우
→ X
- ...

그 외에 다른 변경이라고 할 수 있는 상황이 많을 수가 있다. 그런데 DIP를 하면 위 모든 상황에서 클라이언트는 영향을 받지 않게 된다. **물론 런타임 시점에 논리적인 결함이 발생할 수도 있긴 할 것이다.**

반면에, DIP 없이 직접적인 의존관계를 맺는다고 한다면 곧바로 영향을 받게 되고 사용 관계인 클라이언트의 소스 코드는 모조리 변경되어야 할 것이다.

책에서는 View, Presenter, Controller, Indicator, Database 등 여러 컴포넌트가 있는데 각각의 컴포넌트와 컴포넌트 사이에 인터페이스를 둬서 직접적이변경의 영향으로부터 확실하게 격리하고 있다., 만약 각각의 컴포넌트 사이에 인터페이스가 없다면 추이 종속성을 가지면서 일부 컴포넌트의 변경에 영향이 전파되게 되게 된다. 

추이 종속성을 가진 다는 것은 곳 소프트웨어 엔티티는 자신이 직접 사용하지 않는 요소에는 절대로 의존해서는 안된다라는 소프트웨어의 원칙을 위반하게 되는 것이다.

**추이 종속성**

클래스 A가 클래스 B에 의존하고, 클래스 B가 클래스 C에 의존한다면 클래스 A는 클래스 C에 의존하게 된다.

**수준이란?**

클린 아키텍처에서는 입력와 출력으로부터의 거리라고 정의하고 있다.  비즈니스 로직은 입력과 출력 방식에 변경에 의한 영향도를 최대한 받지 않아야 하므로 고수준에 위치 시켜야 한다. 다시 말해 그 고유의 순수성을 외부의 변화를 부터 보호하기 위함인 샘이다.

OCP의 목표는 시스템을 확장하기 쉬운 동시에 변경으로 인해 시스템이 너무 많은 영향을 받지 않도록 하는데 있다.

# 9장. LSP: 리스코프 치환 원칙

자료형 S가 자료형 T의 하위형이라면 필요한 프로그램의 속성(정확성, 수행하는 업무 등)의 변경 없이 자료형 T의 객체를 자료형 S의 객체로 교체(치환)할 수 있어야 한다는 원칙이다.

예를 들자면, Client란 클래스가 Server란 인터페이스과 사용 관계를 맺고 있을 때 이 Server 인터페이스를 대신해서 다른 구현체로 대체하더라도 정상적으로 동작해야 한다. Client가 Server 인터페이스의 구현체와는 직접적으로 의존하고 있지 않기 때문이다.

이를 위반한 예시로 직사각형/정사각형 문제를 들고 있다. 직사각형을 상속한 정사각형은 동일한 메소드에 대해 다른 방식으로 로직을 수행하므로 대체될 수 없으므로. 직사각형의 자리에는 정사각형이 치환되기가 어렵기 때문이다. (사용자가 원하는 로직이 직사각형인지 정사각형인지를 확인하기 위한 장황한 로직이 추가되어야 한다.

# 10장. ISP: 인터페이스 분리 원칙

**인터페이스 분리 원칙**은 클라이언트가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다는 원칙이다. 

만약 이용하지 않는 메소드에 의존할 경우 변경사항에 발생 했을 때 재컴파일과 재배포가 필요할 수도 있다고 책에서 강조하고 있다.

### ? 조오금 모호하다.

# 11장. DIP: 의존성 역전 원칙

사전적인 정의에 따르면 DIP를 통해 상위 계층(정책 결정)이 하위 계층(세부 사항)에 의존하는 전통적인 의존관계를 반전(역전)시킴으로써 상위 계층이 하위 계층의 구현으로부터 독립되게 할 수 있다.

의존성 역전 원칙을 통해 유연성이 극대화된 시스템을 구축할 수 있으며 의존성이 추상에 의존하며 구체에 의존하지 않는 시스템이다.

그런데 그 의존 관계를 맺는 클래스가 불변성을 가지는 등 안정적이라면 용인한다고 한다. 다시 말해 의존하지 않도록 피하고자 하는 것은 변동성이 큰 구체적인 요소인셈이다.

변경이 가능하고 유연한 특성은 그에 따른 리스크도 함께 따라옴을 알 수 있다.

인터페이스와 이를 구현한 구현체가 있을 때 구현체가 변경됐을 때 인터페이스가 변경될 확률은 없지만, 인터페이스가 변경 됐을 때는 구현체도 변경되어야 한다. 결론적으로 인터페이스에 의존하는게 변동성이 더 낮은 셈이다. 아키텍트는 이 인터페이스의 변경 없이 기능이 추가되도록 하기 위해 노력한다.

실제적인 코딩 실천법은 다음과 같다.

- 변동성이 큰 구체 클래스를 참조하지 말라.
이 제약을 통해 객체 생성 방식에 제약을 걸 수 있고, 추상 팩토리를 사용하도록 강제한다.
- 변동이 큰 구체 클래스로부터 파생하지 말라
구체 클래스로 부터 상속을 받아서 구현을 하게 경우 그 클래스는 슈퍼 클래인 구체 클래스와 직접적인 종속성을 가지게 되고 변경이 어려워 지게 된다.
- 구체 함수를 오버라이드 하지 말라
이전 실천법과 동일한 이유이다.
- 구체적이며 변동성이 크다면 절대로 그 이름을 언급하지 말라

## 팩토리

위 실천법을 준수하려면 객체 생성에 주의해야 한다. 이를 조심하기 위한 방법으로 추상 팩토리가 있다.

![image](https://user-images.githubusercontent.com/58139899/147716229-9da9333f-3ad2-4c7a-b768-3efa1e91dcc7.png)

애플리케이션은 ServiceFactory를 구현한 ServiceFactoryImpl로 ConcreteImpl을 만드는데 이를 Service 타입으로 반환한다. 그렇게 될 경우 애플리케이션은 소스코드에서 구체에 전혀 의존하지 않고 추상적인 것에만 의존하게 된다. 위 사진에 곡선을 기준으로 추상적인 것과 구체적인 것이 완전히 구분되는 셈이다.

또한 위 상황에서 변경이 발생하면 구체적인 부분인 서비스 팩토리 임플과 콘크레이트 임플만 수정이 되면 된다.

제어흐름은 소스 코드 의존성과는 정반대 방향으로 곡선을 가로지르는 것을 알 수 있는데, 소스코드 의존성과 제어흐름이 정반대로 역전 되기 때문에 의존성 역전이라고 한다.
