## 아이템 10. equals는 일반 규약을 지켜 재정의하라

### 재정의 하지 않는 것이 나은 경우
1. 각 인스턴스가 본질적으로 고유하다.
   * 값을 표현하는 게 아니라 동작하는 개체를 표현하는 클래스 &rarr; Thread
2. 인스턴스의 논리적 동치성을 검사할 일이 없다.
3. 상위 클래스에서 재정의한 equals가 하위 클래스에도 딱 들어맞는다. &rarr; Set, List, Map
4. 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없다.
    ```java
   // 실수로라도 호출되는 것을 막고싶다면 아래와 같은 방법으로 구현
   @Override
    public boolean equals(Object o) {
        throw new AssertionError();
    }
    ```
 
### 재정의해야 할 경우
* 객체 식별성이 아니라 논리적 동치성을 확인해야 하는데, 상위 클래스의 equals가 논리적 동치성을 비교하도록 재정의되지 않았을 때
  * 주로 값 클래스가 해당 : Integer, String
  * 인스턴스 통제 클래스라면 값이 같은 인스턴스가 둘 이상 만들어지지 않기 때문에 재정의하지 않아도 된다.
    &rarr; Enum
* 겍체 식별성 : 두 객체가 물리적으로 같은가

### 동치관계
* 반사성
  * 객체는 자기 자신과 같아야 한다. 
  * null이 아닌 모든 참조 값 x에 대해, x.equals(x)는 true다.
* 대칭성
  * 두 객체는 서로에 대한 동치 여부에 대해 같은 결과여야한다. 
  * null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)가 ture면 y.equals(x)도 true다.
* 추이성 : null이 아닌 모든 참조 값 x, y, z에 대해, x.equals(y)가 true이고, y.equals(z)도 true면 x.equals(z)도 ture다.
* 일관성 : null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)를 반복해서 호출하면 항상 true를 반환하거나 항상 false를 반환한다.
* null 아님
  * 모든 객체는 null과 같지 않아야 한다. 
  * null이 아닌 모든 참조 값 x에 대해, x.equals(null)은 false다.

### equals 메서드 구현 방법
1. == 연산자를 사용해 입력이 자기 자신의 참조인지 확인한다.
   * ==(동일성) : 객체 식별성 (주소값 비교)
   * equals(동등성) : 객체가 가진 값 비교
2. instanceof 연산자로 입력이 올바른 타입인지 확인한다.
3. 입력을 올바른 타입으로 형변환한다.
4. 입력 객체와 자기 자신의 대응되는 '핵심' 필드들이 모두 일치하는지 하나씩 검사한다.
5. 대칭성, 추이성, 일관성 확인하기
6. equals를 재정의할 땐 hashCode도 반드시 재정의하자.

### AutoValue 프레임워크 사용해보기