컴포넌트는 배포단위이며, 잘 설계된 컴포넌트라면 독립적으로 배포 가능해야 하고, 독립적으로 개발 가능한 능력을 갖춰야 한다. (작은 단위로 보면 jar, 패키지 일것 같다.)

링커를 통해 컴포넌트로 나누는것이 가능해졌다.

## 컴포넌트의 응집도

### 재사용/릴리스 등가 원칙 (REP)

메이븐에서 사용되는 하나하나의 DEPendy가 재사용/릴리스 등가 원칙을 기본적으로 지키는것 아닐까?

릴리스번호를 매겨서 배포하고, 이것을 서로 호환하는지 버전으로 보증한다.

**이 원칙은 응집성 높은 클래스와 모듈들로 구성되어야 한다.** 단순히 뒤죽박죽으로 구성된 클래스와 모듈로 구성되어서는 안된다.

컴포넌트를 구성하는 모듈은 서로 공유하는 중요한 테마나 목적이 있어야 한다.

## 공통 폐쇄 원칙 (CCP)

동일한 이유로 동일한 시점에 변경되는 클래스를 같은 컴포넌트로 묶어라.

SRP와 비슷하게 생각하며 되고, **해당 원칙은 같은 이유로 변경될 가능성이 있는 클래스는 한 곳으로 묶을것을 권한다**.

마치 인터페이스가 변경되면 구현체들이 다 바뀌니 그모든것을 하나의 컴포넌트로 묶는것 처럼.

⇒ 결국 컴포넌트는 작아지지 않을까 싶음.

## 공통 재사용 원칙(CRP)

컴포넌트 사용자들을 필요하지 않는 것에 의존하게 하지 말아라.

클래스가 서로 강하게 결합되어 있으면 함께 재사용이 된다. 따라서 이들 클래스는 반드시 동일한 컴포넌트에 위치해야 한다.

어떤 컴포넌트가 다른 컴포넌트를 사용하면 두 컴포넌트 사이에는 의존성이 생겨난다.

하나의 클래스만 사용한다고 의존성이 약해지지는 않는다.

의존성이 있으면, 배포되는 순간 다른 컴포넌트도 재배포 되어야 할 가능성이 있다.

즉 CRP는 사용하지 않는 클래스를 가진 컴포넌트에 의존하지 말아야 한다는것.

의미없는 의존은 버려라.

REP, CCP는 포함원칙, CRP는 배제 원칙이다.

## 의존성 비순환 원칙 ADP

컴포넌트 의존성 그래프에 순환이 있으면 안된다.

개발자는 자신만의 공간에서 컴포넌트를 지속적으로 수정하고, 나머지 개발자는 과거에 릴리스된 버전을 사용한다.

새로운 릴리스가 나와도 다른 팀은 이것을 사용할지 여부를 판단한다.

이럴경우 어떤 팀도 다른팀에 의해 좌우되지 않고, 통합은 작고 점진적으로 이뤄진다. 주단위 통합은 사라진다.

이방식이성공하려면 의존성이 생기면 안된다.

이 방법을 사용하면 의존성을 아무리 따라가도 최초의 컴포넌트로 돌아갈 수는 없다.

메인이 새로 릴리스 되어도, 이것으로 인해 다른 컴포넌트는 전혀 영향이 없다.

순환이 되면 릴리스 하는 일이 어렵다. 어디서 부터 빌드를 해야할까..

의존을 끊기위해 DIP를 사용하면 된다. 아니면 서로 의존하는 클래스를 따로 빼어 컴포넌트를 만들면 된다.

애플리케이션은 성장하면서 컴포는터 의존성 구조는 흐트러질것인데, 이것은 다시고쳐진다.

기본적으로 하향식으로 설계가 불가능하다는것이 느껴진다.

아무런 클래스도 설계하지 않은 상태에서 컴포넌트 의존성 구조를 설계하려고 하면 실패할 수 있다.

## 안정된 의존성 원칙

컴포넌트가 다른 유형의 변경에는 향을받지 않으면서도 특정 유형의 변경에만 민감하게 만들 수 있다.

변경이 쉽지 않은 컴포넌트가 변동이 예상되는 컴포넌트에 의존하게 만들어서는 절대로 안된다.

당신이 모듈을 만들 때 변경하기 쉽도록 만들었지만, 모듈에 누군가가 의존성을 달아버리면 모듈 변경을 어려워진다.

동전을 세워놓은것은 불안정하다. 하지만 탁자를 세워논건 안정적이다. 이유는 탁자를 뒤집기는 어렵기 때문이다.

소프트웨어의 변경을 어렵게하는것은 다른 의존성이 많아지게 하면 되는것이다.

모든 컴포넌트가 최고로 안정적인 시스템이라면 변경이 붉가능하다. 이는 바람직하지 않고, 우리가 컴포넌트를 설계할 때 기대하는것은 불안정한 컴포넌트도 있고, 안정적인 컴포넌트도 존재하는 상태이ㅏㄷ.

## 안정된 추상화 원칙

고수준은 자주 변경되는것이라 생각하면 되는데, 고수준 정책을 캡슐화하는 소프트웨어는 반드시 안정된 컴포넌트에 위치해야 한다.

하지만 고수준 정책을 안정된 컴포넌트에 위치시키면, 그 정책을 포함하는 소스 코드는 수정하기가 어려워진다.

컴포넌트가 안정적이면서 동시에 변경에 충분히 대응할 수 있을 정도로 유연하게 만들려면 OCP를 하면된다.

따라서 안정적인ㅋ ㅓㅁ포넌트라면 반드시 인터페이스와 추상 클래스로 구성되어 쉽게 확장할 수 있어야 한다.

실제로 SDP에서는 의존성이 반드시 안정성의 방향으로 향해야 한다고 말하며, SAP에서는 안정성이 결국 추상화를 의미한다고 말한다.

따라서 의존성은 추상화의 방향으로 향하게 된다.

추상적이지 않은 영역을 고통의 영역이라 부르는데, 데이터베이스 스키마나 엔티티가 이 구간에 속한다.

또는 유틸 클래스도 이 영역에 속한다. 변동성이 없는것은 이 구역에 있어도 해롭지 않다. 변동될 가능성이 거의 없ㄷ기 때문이다

쓸모없는 영역은 구현하지 않은 채 남겨진 추상 클래스인 경우가 많다.
