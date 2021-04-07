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
