# 함수

> 함수의 기본 구조
```kotlin
fun 함수명(파라미터 이름: 타입): 반환타입 {
  return 값
}
```

> 함수 예시  
```kotlin
// 반환값, 입력값이 있는 함수
fun square(x: Int): Int{
  return x*x
}

// 반환값이 없는 함수
fun printSum(x: Int, y: Int){
  Log.d("fun","x+y=${x+y}")
}

//입력값이 없는 함수
fun getPi(): Double{
  return 3.14
}
```

# 클래스

> 기본 구조
```kotlin
class 클래스명 {  
  var 변수
  fun 함수(){
    //코드
  }
}
```
> 생성자
- primary 생성자    
: 클래스의 헤더처럼 사용   
```kotlin
class Kotlin_ex constructor(value: String){
  //code
}
//접근제한자나 특정 옵션이 없으면 constructor 키워드 생략가능
```
- secondary 생성자   
: 함수처럼 사용
```kotlin
class kotlint_ex2 {
  constructor (value: String){
    Log.d("class","생성자로부터 전달받은 값은 ${value} 입니다.")
  } 
}
```
- companion object   
: 클래스를 인스턴스화 하지 않고 사용   
: Log클래스의 메서드 d(),e() 모두 companion object코드로 만들어져 있어 생성자 없이 바로 호출해서 사용가능  

# data class
: 간단한 값 저장 용도  
: 생성자와 달리 파라미터 앞에 var 또는 val을 명시해서 변수인지 상수인지 구분해야 함   

```kotlin
// 일반 클래스에서 toString() 호출시 주소값 반환
// 데이터 클래스는 값 반환
data class DataUser (var name: String, var age:Int)
var dataUser = DataUser("Michael",21)
Log.d("DataClass","DataUser는 ${dataUser.toString()}")

// copy 메서드 지원
```
![image](https://user-images.githubusercontent.com/50178026/113859169-90562d00-97df-11eb-96f7-e2ac0ede07cd.png)

# 상속, 확장

> 상속
```kotlin
// 부모 클래스는 open 키워드로 만들어야 자식 클래스에서 사용가능
open class Parent{
  var hello: String = "안녕하세요."
      fun sayHello(){
        Log.d("inheritance","${hello}")
      }
}
// 부모 클래스명 다음에 괄호를 입력해서 생성자 호출
class child: Parent(){
  fun myHello(){
    hello = "Hello!"
    sayHello()
  }
}
```
> 오버라이드
: 상속받은 부모 클래스의 프로퍼티와 메서드 중에 자식 클래스에서는 다른 용도로 사용해야하는 경우 사용  
```kotlin
// method override
// 상속할 메서드 앞에 open 키워드를 붙이면 오버라이드 가능
open class BaseClass{
  open fun opened(){
  }
  fun notOpend() {
  }
}

class ChildClass : BaseClass(){
  override fun opened() {
  }
  //open이 없으므로 오버라이드 불가
  override fun notOpend(){
  }
}

//property override
open class BaseClass2 {
  open var opened: String = "I am"
}
class ChildClass2: BaseClass2() {
  override var opened: String = "You are"
}

//extensions
//실제 코드가 변경되는 것은 아님
fun classname.확장할 함수 () {
  //code
}
```
# 설계 도구

> 추상화
: 개념 설계 단계에서 메서드 이름만 작성
: 구현 단계에서 추상화된 크래스를 상속받아서 아직 구현되지 않은 부분을 마저 구현함  

```kotlin
//추상화
//abstract 이용
abstract class Animal {
  fun walk() {
    Log.d(tag, "걷습니다.")
  }
  abstract fun move()
}

//구현
class Bird: Animal() {
  override fun move() {
    Log.d(tag, "날아서 이동")
  }
}
```
> 인터페이스
: 실행 코드 없이 메서드 이름만 가진 추상 클래스  
: 인터페이스 남용하면 코드의 가독성, 효율성 떨어짐

```kotlin
interface InterfaceKotlin {  
  var variable: String  
  fun get()  
  fun set()
}

// 클래스에서 구현
// 생성자 호출하지 않고 인터페이스 이름만 지정
class KotlinImpl: InterfaceKotlin {
  override var variable: String = "init value"
  override fun get() {
    //code
  }
  override fun set() {
    //code
  }
}

// 상속 형태가 아닌 직접 구현
// object사용
var kotlinImpl = object: InterfaceKotlin {
  override var variable: String = "init"
  override fun get() {
    //code
  }
  override fun set() {
    //code
  }
}
```
> 접근 제한자

접근 제한자 | 제한 범위
:---------:| :---------:
private    | 다른 파일에서 접근할 수 없음
internal   | 같은 모듈에 있는 파일만 접근 가능
protected  | private과 같으나 상속 관계에서 자식 클래스가 접근 가능
public     | 제한 없이 모든 파일에서 접근 가능

> 제네릭
: 입력되는 값의 타입을 자유롭게 사용하기 위한 설계 도구

```kotlin
public interface MutableList<E>{
  var list: Array<E>
}
//<E> 부분에 String과 같은 특정 타입이 지정되면 클래스 내부에 선언된 모든 E에 String 타입으로 지정
```

# Null Safety
> Nullable

- ?  
```kotlin
//null 값 허용
// 변수 타입 뒤에 ? 입력
var variable: String?
``` 
- ?.  
: 해당 변수가 null일 경우 ?. 다음의 메서드나 프로퍼티를 호출하지 않음    

```kotlin
fun testSafeCall(str: String?): Int? {
  //str이 null이면 lenght 실행되지 않고 null 반환
  var resultNull: Int? = str?.length
  return resultNull
}
```
- ?:  
: 해당 변수가 null일 경우 ?: 오른쪽 값 반환 
```kotlin 
fun testElvis(str: String?): Int {
  // legnth 오른쪽에 ?:을 사용하면 str이 null일 경우 0이 반환
  var resultNonNull: Int = str?.length?:0
  return resultNonNull;
}
```




