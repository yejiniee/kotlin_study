

__'Android Studio'로 실습시 MainActivity.kt 파일에 override fun onCreate 함수 밑에 코드를 작성할 것__


# 로그와 로그캣

* 로그 : 코딩시 코드의 흐름을 파악하기 위해 앱 외부에 출력하는 정보. 코드 중간중간 사용하면, 앱의 실행 흐름 혹은 결과값을 확인할 수 있음.
* 로그캣 : 출력되는 로그를 모아서 보는 도구, 태그를 필터로 특정 로그 확인 가능.

함수 | 의미 | 내용
-----|-----|---
 Log.v() | verbose | 상세한 로그 내용 출력
 Log.d()| debug | 개발에 필요한 내용 출력(개발자용)
 Log.i()| information | 정보 전달
 Log.w() | warning | 경고 메세지 전달
 Log.e() | error | 에러 메세지 전달
 
 ```kotlin
 Log.d("Tag", "Message")
 ```
# 자료형

데이터 타입 | 설명
-----------|-----
Double | 8bytes
Float | 4Bytes
Long | 8Bytes
Int | 4Bytes
Short|2Bytes
Byte | 1Byte
Char | 1개의 문자
String | 문자열
Boolean | true or false

 
# 변수 

  * var : 값 재할당 가능 
    
    ```kotlin
    //선언과 동시에 초기화
    var name: String = "Hansu"
    //선언 후 초기화
    var name: String
    name = "Hansu"
    ```
  
  * val : 읽기 전용 변수 (상수랑 비슷)
        : 값 변경 불가
  
  ```kotlin
  val language = "kotlin"
  //에러
  language = "java"
  ```
  
  * const : 상수, val 앞에 붙여 사용
          : 값 변경 불가
          : 기본형(Int, Long 등)과 문자열만 입력가능
   
  ```kotlin
  const val PI = 3.141592
  ```
  
# ☆☆☆ 컨벤션 ☆☆☆

* 컨벤션(Convention) : 코드를 작성하는 규칙 ex)prettier

* Camel Case
    + 클래스명 : 첫글자, 새로운 단어의 첫글자를 대문자로 한다.
    ```kotlin
    class MainActivity
    ```

    + 함수, 변수명 : 첫글자는 소문자, 새로운 단어의 첫글자는 대문자로 한다.
    ```kotlin
    fun onCreateActivity()
    var intValue: Int
    ```

    + 상수명 : 모두 대문자로 작성한다. (val은 상수가 아니다)
    ```kotlin
    const val HELLO: String = "안녕"
    //snake case
    const val HOW_ARE_YOU: String = "어떻게 지내?"
    ```

* Snake case
    + underbar(\_)를 이용하여 가독성이 좋다
    + 상수명만 대문자를 사용, 나머지는 소문자
    ```kotlin
    fun on_create_activity()
    ```
 
  
  
  
