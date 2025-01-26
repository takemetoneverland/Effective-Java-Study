## 아이템 12. toString을 항상 재정의하라

### toString은 그 객체가 가진 주요 정보 모두를 반환하는 것이 좋다.
* 하위 클래스들이 공유해야 할 문자열 표현이 있는 추상 클래스라면 toString을 재정의해줘야 한다.
* toString을 재정의한 클래스는 사용하기 편하고 디버깅하기 쉽게 해준다.
* toString은 해당 객체에 관한 명확하고 유용한 정보를 읽기 좋은 형태로 반환해야 한다.

```java
/**
 * 전화번호의 문자열 표현을 반환
 * 이 문자열은 "XXX-YYY-ZZZZ" 형태의 12글자로 구성된다.
 * XXX는 지역코드, YYY는 프리픽스, ZZZZ는 가입자 번호다.
 * 전화번호의 각 부분의 값이 작아서 자릿수를 채울 수 없다면, 앞에서부터 0으로 채운다.
 */
@Override
public String toString() {
    return String.format("%03d-%03d-%04d", areaCode, prefix, lineNum);
}
```