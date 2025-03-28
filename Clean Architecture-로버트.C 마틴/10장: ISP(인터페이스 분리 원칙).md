# 📕 ISP 인터페이스 분리 원칙
인터페이스 분리 원칙(ISP)은 아래 다이어그램에서 그 이름이 유래했다.  

<img src="../Clean Architecture-로버트.C 마틴/img/10_1.png" alt="설명" width="500" style="display: block; margin: auto;">

여기서 다수의 사용자가 `OPS` 클래스의 오퍼레이션을 사용한다.  
- User1은 `op1`만 사용  
- User2는 `op2`만 사용  
- User3은 `op3`만 사용  

그러나 `OPS`가 정적 타입 언어로 작성된 클래스라면,  
`User1`은 `op2`와 `op3`를 전혀 사용하지 않음에도 불구하고,  
이 두 메서드에 의존하게 된다.  

따라서 **OPS 클래스에서 `op2`의 코드가 변경되면,  
`User1`도 다시 컴파일하고 새로 배포해야 하는 문제**가 발생한다.  

이러한 문제는 **오퍼레이션을 인터페이스 단위로 분리하여 해결**할 수 있다.  

<img src="../Clean Architecture-로버트.C 마틴/img/10_2.png" alt="설명" width="500" style="display: block; margin: auto;">

정적 타입 언어에서 위 다이어그램처럼 **인터페이스를 분리**하면,  
`User1`은 **U1Ops 인터페이스와 `op1`만 의존하고, `OPS`에는 의존하지 않게 된다.**  

결과적으로,  
- `OPS`에서 변경이 발생해도 **User1과 관계없는 변경이라면, User1을 다시 컴파일하거나 배포할 필요가 없다.**  
- 이는 **불필요한 의존성을 제거하고, 변경의 영향을 최소화하는 효과**를 가져온다.  

인터페이스 분리 원칙을 적용하면 **각 사용자가 필요한 기능만 의존하도록 만들 수 있으며,  
이로 인해 시스템의 유연성과 유지보수성이 향상된다.**  

## 📗 ISP와 언어
정적 타입 언어에서는 **소스 코드에 포함된 선언문**으로 인해  
**소스 코드 의존성이 발생**한다.  

반면, 루비나 파이썬과 같은 동적 타입 언어에서는  
이러한 선언문이 존재하지 않으므로, 소스 코드 의존성이 없다.  
따라서 재컴파일과 재배포가 필요하지 않다.  

이러한 특성 덕분에, **동적 타입 언어를 사용하면  
정적 타입 언어보다 유연하고 결합도가 낮은 시스템**을 만들 수 있다.  

이 사실을 고려하면,  
**ISP(인터페이스 분리 원칙)는 아키텍처의 문제가 아니라,  
언어의 특성과 관련된 문제로 볼 여지가 있다.**  

## 📗 ISP와 아키텍처
다음과 같은 의존 관계를 가진 시스템이 있다고 가정하자.  

**|System S| → |Framework F| → |Database D|**  

여기서 시스템 S는 프레임워크 F를, F는 데이터베이스 D를 의존한다.  

그러나 F에는 S와 전혀 관계없는 불필요한 기능이 D에 포함될 수 있다.  
이 경우, D 내부가 변경되면 F를 재배포해야 할 수도 있으며,  
이는 결국 S까지 재배포해야 하는 상황을 초래할 수 있다.  

즉, **ISP(인터페이스 분리 원칙)를 지키지 않으면,  
의존성으로 인해 불필요한 변경이 연쇄적으로 영향을 미칠 위험이 커진다.**  

## 📗 결론
불필요한 짐을 실은 무언가에 의존하면 예상치도 못한 문제에 빠진다는 사실이 ISP에서 배울수 있는 교훈이다.