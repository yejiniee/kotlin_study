# 함수

### 함수의 정의

* 안드로이드 앱은 onCreat()함수를 호출해서 실행된다.
* 파라미터와 반환값이 없는 함수도 있을 수 있다.
* 최상위 자료형 Any
* 반환 값이 없을 시 자료형 Unit

```kotlin
fun 함수명(파라미터 이름: 타입): 반환 타입 {
  return 값
}
//반환 값이 없을 경우
fun printSum(x: Int, y: Int) {
  Log.d("fun", "x + y = ${x + y}")
}
```

### 함수의 파타미터

```kotlin
// 코틀린에서의 함수 파라미터는 모두 val이 생략된 형태라고 생각하자.  
fun 함수명(name1: String, name2: Int, name3: Double) { } //val이 생략되어 있다.

// 파라미터의 디폴트(기본값) 설정  
fun 함수명(name1: String, name2: Int = 157, name3: Double) { } //name2는 따로 인자를 받지 않을 경우 157로 취급한다.

//따로 파라미터 값을 입력하고 싶은 경우
함수명(name3 = 1.07) // 과 같이 해당 파라미터 이름에 직접 값을 넣어준다.
```

# 클래스

* 기본구조

```kotlin
class 클래스명 {
  var 변수
  fun 함수() {
  }
}
```
* 대부분의 코드는 클래스 스코프 안에 작성된다.

### 생성자

##### init함수 : 생성자 호출시 실행되는 함수
```kotlin
class Person(value: String) {
  init {
    Log.d("class", "생성자로부터 전달받은 값은 ${value}입니다.")
  }
}
```

* Primary
  + 별다른 옵션이 없다면, constructor와 같은 키워드 생략가능.

```kotlin
class Person Primary() {
}
//ex
class Person constructor(value: String) {
}
//ex2
class Person(value: String) { //이렇게 쓰자.
}
```

* Secondary
  + constructor를 스코프 안에 직접 작성
  + 파라미터의 개수 또는 타입이 다르다면 여러개 생성이 가능하다.

```kotlin
//여러개 생성가능, Primary가 있어도 생성가능
class Person {
  constructor(value: String) {
  }
  constructor(value: Int) {
  }
 ```

* Default(기본 생성자)
  + 생성자를 작성하지 않을 경우, 파라미터가 없는 Primary생성자가 하나 있는 것과 동일
  + init함수 실행됨


### 클래스의 사용

##### 클래스명()

* 생성자를 호출하면 인스턴스가 생성된다.
* 인스턴스는 변수에 담을 수 있다.
* 클래스 내부의 메서드와 프로퍼티는 도트연산자(.)을 사용해서 참조할 수 있다.

`var kot = Kotlin()`


#### 프로퍼티와 메서드

* 클래스 내부의 변수 = 프로퍼티(Property)
  + 클래스의 함수 안에서 정의된 변수는 프로퍼티라고 하지 않는다.
* 클래스 내부의 함수 = 메서드(Method)
  
### data class

* 간단한 값의 저장 용도
* var, val 생략 불가.

```kotlin
data class 클래스명 (val 파라미터1: 타입, var 파타미터2: 타입)
//ex
data class UserData(val name: String, var age: Int)
var userData = UserData("Michael", 21)
```

#### toString(), copy()

* 일반 클래스에서는 주소값을 반환하지만, data class에서는 값을 반환한다.

```kotlin
Log.d(tag, "UserData는 ${userData.toString()}")
//결과
"UserData는 UserData(name=Michael, age=21)"
```
* copy로 값 복사 가능
```kotlin
var newData = userData.copy()
```

# 클래스의 상속과 확장

* open 으로 상속할 수 있게 함(부모 클래스)
* 상속은 부모의 인스턴스를 자식이 갖는 과정 (부모 클래스명 뒤에 소괄호로 생성자를 호출해야함)

```kotlin
open class 상속될 부모 클래스 { //부모는 자식클래스의 함수, 변수 사용불가 }
class 자식 클래스: 부모 클래스() { //부모 클래스 뒤에 ()를 입력해 생성자를 반드시 호출해야함.
  //자식은 부모클래스의 함수, 변수 사용가능 
}
//파라미터가 있는 경우
open class 부모(value: String) {}
class 자식(value: String): 부모(value) {}
```

* Secondary의 경우 자식클래스의 secondary 생성자에서 super로 사용가능
* Secondary생성자를 이용하는 경우에는 부모 클래스 다음 괄호 생략가능

```kotlin
class CustomView: View {
  constructor(ctx: Context): super(etx)
  constructor(ctx: Context, attrs: AttributeSet): super(ctx, attrs)
}
```
* 자식은 부모 클래스의 프로퍼티와 메서드 사용가능

### 오버라이드

* 부모에게 물려받은 프로퍼티와 메서드를 재정의
* 앞에 open을 붙혀 오버라이드

```kotlin
//Method Override
open class BaseClass {
  open fun opened() {}
}
class ChildClass: BaseClass() {
  override fun opened() {}
}
//Property Override
open class BaseClass2 {
  open var opened: String = "I am"
}
class ChildClass2: BaseClass2() {
  override var opened: String = "You are"
}
```

#### 익스텐션(Extensions)

* 클래스, 메섣, 프로퍼티에 대한 Extensions 지원.
* 이미 만들어져 있는 클래스에 메서드 추가
* 누군가 작성해둔, 이미 컴파일 되어있는 클래스에 메서드를 추가하기 위한 용도

`fun 클래스.확장할메서드() {}`

```kotlin
class MyClass P
  fun say()
  fun walk()
  fun eat()
}
//sleep() 메서드 추가
MyClass.sleep() {}//혹은 fun myClass.sleep() {}
//함수 정의와 동시에 익스텐션. (plus함수)
fun String.plus(word: String): String {
  return this + word
}
```

* 실제 코드가 변경되는 것이 아니며, 실행시에 사용가능하게 해주는 것 뿐.

# object
##### (자바의 static)

* 클래스를 생성자로 인스턴스화 하지 않아도 프로퍼티와 메서드 호출가능
* object는 클래스와 다르게 앱전체에 1개만 생성가능
* 상수(const)는 object 안에서만 사용할 수 있다.
```kotlin
object Pig {
  var name: String = "Pinky"
  fun printName() {
    Log.d("class", "Pig의 이름은 ${name}입니다.")
  }
}
```
### companion object

* class 내부에 companion object를 선언.
* companion object부분은 그냥쓰일 수 있지만, 나머지 부분은 생성자를 호출한 후 사용가능

```kotlin
class Pig {
  companion object {
    var name: String = "None"
    fun printName() {
      Log.d("class", "Pig의 이름은 ${name}입니다.")
    }
  }
  fun walk() {  //이 부분은 생성자를 호출해야 사용가능하다.
    Log.d("class", "Pig가 걸어갑니다.")
  }
}
```  
  
# 설계

* 파일을 분류하고, 이름을 짓고, 디렉터리에 모아 놓는 것 모두 설계
* 객체지향 프로그래밍 = 구현(실제 로직을 갖는코딩) + 설계(껍데기만 있는 코딩)

## 패키지

* 패키지는 클래스와 소스파일을 관리하기 위한 디렉터리 구조의 저장 공간
* 서브디렉터리 안에 실제 클래스.kt 파일이 있다
* 관계가 있는 파일을 동일한 패키지에 만들어두면 관리 용이

```kotlin
package 메인디렉터리.서브디렉터리.서브디렉터리2
class 클래스명 { ... }
```

## 추상화

* 설계단계에서 클래스의 이름과 클래스 안에 있음 직한 기능을 유추해서 나열
* 구현 클래스는 이 추상 클래스를 __상속__ 받아서 추상화 기능을 '모두' 구현해주어야함
* abstract 키워드 사용

```kotlin
//설계
abstract class Animal {
  fun walk() {
    Log.d(tag, "걷습니다.")
  }
  abstract fun move()
}
//구현
class Bird: Animal() {
  override fun move() {
    Log.d(tag, "날아서 이동합니다.")
  }
}
```

## 인터페이스

* 실행 코드 없이 메서드 이름만 가진 추상 클래스
* 즉, 실행 코드가 한 줄이라도 있으면 추상화, 코드 없이 메서드 이름만 나열되어 있으면 인터페이스
* 상속 관계의 설계보다는 __외부 모듈에서 내가 만든 모듈을 사용할 수 있도록__ 메서드의 이름을 나열해둔 일종의 명세서 개념

```kotlin
interface InterfaceKotlin {  //class 키워드는 사용되지 않는다.
  var variable: String  //코틀린에서'만' 프로퍼티를 인터페이스 내부에서 정의할 수 있다.
  fun get()  //인터페이스의 프로퍼티와 메서드 앞에는 abstract가 생략되어 있다.
  fun set()
}
```

* 구현시 생성자를 호출하지 않아도 됨.

```kotlin
//상속으로 구현
class KotlinImpl: InterfaceKotlin {
  override var variable: String = "init value"
  override fun get() { ... }
  override fun set() { ... }
}
//상속 형태가 아닌 직접 구현, object사용
var kotlinImpl = object: InterfaceKotlin {
  override var variable: String = "init"
  override fun get() { ... }
  override fun set() { ... }
} //실제로 자주 사용하는 형태 
```
* 안드로이드가 봤을 때 개발자가 만드는 모듈은 외부모듈이기 때문에 인터페이스를 자주 사용한다.
* 인터페이스를 남용하면 코드의 가독성과 구현 효율성이 떨이잔다.

## 접근 제한자

접근 제한자 | 제한 범위
:---------:| ---------
private    | 다른 파일에서 접근x
internal   | 같은 모듈에 있는 파일만 접근가능
protected  | private와 같으나 자식 클래스가 접근가능
public     | 모든 파일에서 접근가능

* 코틀린에서 모듈이란 한 번에 같이 컴파일되는 모든 파일을 말한다. 즉 하나의 앱이나 라이브러리를 말한다.

```kotlin
open class Parent {
  private val privateVal = 1
  protected open val protectedVal = 2
  internal val internalVal = 3
  val defaultVal = 4
}
//상속
class Child: Parent() {
  fun callVariables() {
    //privateVal은 호출 불가
    //protected, internal, default는 호출 가능
  }
}
//상속관계가 아닌 외부 클래스에서 사용시 public과 internal만 사용 가능하다
```

## 제네릭(Generics)

* 입력되는 값의 타입을 자유롭게 사용하기 위한 설계 도구
* 보통 T부터 U,V,W 순으로 쓴다.

```kotlin
public interface MutableList<E> {
  var list Array<E>
}

var list: MutableList<제네릭> = mutableListOf("월", "화", "수")

fun testGenerics() {
  var list: MutableList<String> = mutableListOf()
  list.add("월")
  list.add("화")
  list.add("수")
  for (item in list) {
    Log.d(tag, "list에 입력된 값은 ${item}입니다.")
  }
}
```

# Null Safety

* Kotlin은 Null에 대해서 안전한 언어

### nullable

* 타입 뒤에 ? 를 붙힌다.

```kotlin
var nullable: String? // ?를 붙이지않으면 오류
nullable = null
```

* null 허용 설정

```kotlin
fun nullParameter(str: String?) {
  if (str != null) {  // 파라미터에서 null이 허용되었기 때무에, 함수 내부에서 if문으로 null체크를 해야 파라미터 사용이 가능하다.
    var length2 = str.length
  }
}
```

### 안전한 호출 (?.) : Safe Call

* Nullable 변수 다음에 ?. 을 사용하면 다음에 오는 메서드 혹은 프로퍼티를 호출하지 않는다

```kotlin
fun testSafeCall(str: String?): Int? {
  //str이 null이면 lenght 실행x, null 반환
  var resultNull: Int? = str?.length
  return resultNull
}
```

### Null 값 대체 (?:) : Elvis Operator

* 선언된 nullable변수나 프로퍼티 다음에 ?: 표기
* 변수가 null이면 ?: 다음에 오는 값을 기본(default)값으로 사용

```kotlin
fun testElvis(str: String?): Int {
  // legnth 오른쪽에 ?:을 사용하면 str이 null일 경우 0이 반환된다.
  var resultNonNull: Int = str?.length?:0
  return resultNonNull;
}
```




