## 아이템 13. clone 재정의는 주의해서 진행하라

* Cloneable : 복제해도 되는 클래스임을 명시하는 용도의 인터페이스
* clone 메서드가 선언된 곳이 Cloneable이 아닌 Object이고, protected이므로 Cloneable을 구현하는 것만으로는 외부 객체에서 clone 메서드를 호출할 수 없다.

### clone 메서드의 일반 규약
* 원본 객체에 아무런 해를 끼치지 않느 동시에 복제된 객체의 불변식을 보장해야한다.
* x.clone() != x
* x.clone().getClass() == x.getClass()
* x.clone().equals(x) &rarr; 일반적으로 참이지만 필수는 아니다.
* x.clone().getClass() == x.getClass()