# 함수
* 함수의 정의
```kotlin
fun 함수명(파라미터 이름 : 타입): 반환타입 {
  return 값
}


//반환값과 입력값이 있는 함수
fun square(x: Int): Int{
  return x*x
}

//반환값이 없는 함수
fun printSum(x: Int, y: Int){
  Log.d("fun", "x + y = ${x+y}")
}

//입력값없이 반환값만 있는 함수
fun getPi(): Double{
  return 3.14
}
```

* 함수 파라미터의 정의
```kotlin
fun 함수명(name: String, age: Int=29, weight:Int=65.5){
  //age와 weight의 기본값을 미리 입력해줌
}
```

# 클래스와 설계

* 클래스의 기본 구조
```kotlin
class 클래스명 {
  var 변수
  fun 함수() {
    //코드
  }
}  
```
* 클래스의 생성
```kotlin
class Kotlin{
  init{
    //생성자가 없으면 아무것도 없는 init 블록이 실행된다.
  }
}

//프라이머리 생성자
class KotlinOne constructor(value: String){  //constructor는 생략가능
  init{
    Log.d("class", "생성자로부터 전달받은 값은 ${value}입니다.")
}

//세컨더리 생성자: constructor 키워드를 함수처럼 사용할 수 있다.
class KotlinTwo{
  constructor (value: String){
  Log.d("class", "생성자로부터 전달받은 값은 ${value}입니다.")
}
```

* 클래스의 사용
```kotlin
var kotlin = Kotlin() //클래스의 생성자를 호출한 후 생성되는 것을 인스턴스라고 한다. 
                      //생성된 인스턴스는 변수에 담을 수 있음.

var one= KotlinOne("value")


class KotlinFour {
  companion object {  //companion object: 클래스를 인스턴스화 하지 않고 사용하기
    var one: String = "None"
    fun printOne() {
      Log.d("class", "one에 입력된 값은 ${one}입니다.")
    }
  }
} 

///companion object 코드불록 안의 프로퍼티와 메소드는 "클래스명"에 도트를 붙여서 생성자 없이 직접 호출가능
KotlinFour.one="새로운 값"
KotlinFour.printOne()
```

* 데이터 클래스

```kotlin
data class DataUser (var name: String, var age: Int) //데이터클래스 생성
var dataUser = DataUser("Michael",22)
Log.d("DataClass", "DataUser는 ${dataUser.toString()}") //DataUser는 DataUser(name=Michael, age=22)

var newData= dataUser.copy() //값 복사
```

* 클래스의 상속
-상속 대상이 되는 부모 클래스는 open 키워드로 만들어야만 자식 클래스에서 사용할 수 있다.
```kotlin
open class Parent {
  var hello: String="안녕하세여"
  fun sayHello() {
    Log.d("inheritance", "${hello}")
  }
}

class Child : Parent() {
  fun myHello() {
    hello = "Hello!"
    sayHello() // 부모클래스에서 상속받은 메서드
  }
}

//부모 클래스의 세컨더리 생성자를 이용하는 경우는 부모 클래스명 다음에 오는 괄호 생략, super() 사용
class CustomView : View { // View클래스를 상속받는 예제
  constructor(ctx: Context): super(ctx)
  constructor(ctx: Context, attrs: AttributeSet): super(ctx, attrs)
}

//오버라이드: 프로퍼티와 메서드의 재정의, 오버라이드 할 때는 프로퍼티나 메서드도 클래스처럼 앞에 open을 붙여야한다.

//메서드 오버라이드
open class BaseClass {
  open var opened: String = "I am"
  open fun opened() {
  }
  fun notOpened{
  }
}

class ChildClass: BaseClass() {
  override var opened: String = "You are"
  override fun opened() {
  }
  //fun notOpened()는 오버라이드 불가능
}

//익스텐션: 미리 만들어져있는 클래스에 메서드를 붙여넣는다.
class MyClass{
  fun say()
  fun walk()
  fun eat()
}

fun Myclass.sleep(){
  //코드
}



```
---->p. 168까지
