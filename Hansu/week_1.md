

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
 //import android.util.Log 필요
 Log.d("Tag", "Message")
 ```
# 자료형

* 자동타입추론

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

 * 사용법 : Double quote(") 안에 ${변수}를 넣어서 사용

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

# 조건문
 
 1. if : 범위가 넓고, 값을 특정할 수 없을 때    ex)연도
 2. when : 범위가 제한되고 값을 특정할 수 있을 때    ex)요일
 
 * 변수if문
     + if의 마지막 줄의 값이 변수에 할당됨
     ```kotlin
     var a = 5
     var b = 3
     var bigger = if (a > b) {
         var c = 30
         a //마지막 값
     } else {
         b //마지막 값
     }
     //a나 b가 bigger에 저장, (a > b) == true 이므로 bigger = a
     Log.d(tag, "Bigger is ${bigger}")
     //결과 : Bigger is 5
    ```
  
  * when : switch와 비슷
  
  ```kotlin
  when (parameter) {
      비교값1 -> {} //한 줄일 경우 중괄호는 없어도 됨
      비교값2 -> {}
      ...
      else -> {} //switch의 default랑 비슷
  }
  ```
  
   + 콤마로 구분해서 사용
      
      ```kotlin
      when (now) {
          8, 9 -> Log.d(tag, "현재 시간은 8시 또는 9시입니다.")
          else -> Log.d(tag, "현재 시간은 9시가 아닙니다.")
      }
      ```
      
      + 범위 값 비교
      
      ```kotlin
      when (age) {
          in 10..19 -> Log.d("when", "10대입니다.") // age가 10이상 19이하
          !in 10..19 -> Log.d("when", "10대가 아닙니다.")
          else -> Log.d("when", "나이를 알 수 없습니다.") // 실수 값을 받지 않은 경우
      }
      ```
      + non-parameter
      
      ```kotlin
      when {
          time == 5 -> Log.d("when", "현재시간은 5시입니다.")
          time > 5 -> Log.d("when", "현재시간은 5시가 넘었습니다.")
      }
      ```
      
# 배열

__index의 시작은 0부터__


`var 변수 = 타입Array(개수) //StringArray는 없다.`

* 배열에 값 할당하기

```kotlin
//문자열 배열의 경우 이렇게 사용한다.
var stringArray = Array(10, {item->""}) //Array의 크기는 10이고 element들을 빈공간으로 채운다.

//함수 사용 (arrayOf)
var dayArray = arrayOf("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
```

* 배열에 값 입력, 수정
    1. 배열명[idx] = element
    2. 배열명.set(idx, element) // set함수 사용


* 배열에 있는 값 꺼내기
    1. 배열명[idx]
    2. 배열명.get(idx) // get함수 사용
     
# 컬렉션

1. 리스트
2. 맵
3. 셋

`mutable : 변할 수 있는, immutable : 변할 수 없는`

기본 함수 | 기능 | 적용가능 컬렉션
--------|-------|-------
add | 값 추가 | list, set
get | 값 사용 | list, map
set | 값 수정 | list, 
removeAt | idx 삭제| list
remove | 값 삭제 | set, map(list도 될듯?)
put | 키, 값 추가 | map




* 리스트(List) : 동적 배열이라고 생각하자. 중복허용
```kotlin
//리스트 생성
var mutableList = mutableListOf("Mon", "Tue", "Wed")
//값 추가, 리스트의 크기가 하나 증가하고 값이 추가된다.
mutableList.add("Thu")
//값 사용(get(idx))
var a = mutableList.get(1)
//값 수정(set)
mutableList.set(1, "수정할 값")
//값 제거(인덱스), 해당 인덱스가 없어지고 뒤의 인덱스들이 한 칸씩 앞으로 간다.
mutableList.removeAt(idx)
//빈 리스트
//var 변수명 = mutableListOf<element의 타입>()
var stringList = mutableListOf<String>()
//컬렉션 개수 가져오기
mutableList.size  // size는 함수가 아닌 프로퍼티이다. (괄호가 필요없기때문)
```

* 셋(Set) : 종복을 허용하지 않는 동적 배열

```kotlin
//빈 셋 생성
var set = mutableSetOf<String>()
//값 추가
set.add("JAN")
set.add("FEB")
set.add("JAN") // 중복 -> 입력되지 않는다.
//셋 사용, 인덱스로 조회 불가, 셋을 통째로 출력
Log.d("Collection", "Set 전체 출력 = ${Set}")
//값 삭제
set.remove("FEB")
```

* 맵(Map) : `Key : Value` 로 이루어짐.  
          : Key = index로 보자.  
          : 동적 배열이라고 생각하자.


```kotlin
//맵 생성
var map = mutableMapOf<String, String>()
//키, 값 추가
map.put("zl", "rkqt")
```
__put 사용시 동일한 키를 가진 값이 있으면 해당하는 키의 값만 수정

```kotlin
//값 사용
map.get("키") //로 값을 꺼낼 수 있다.
//키 삭제
map.remove("키")
```

* Immutable Collection
    + 입력된 값 변경 불가능
    + 수정, 추가, 제거 불가능
    
    ```kotlin
    val IMMUTABLE_LIST = listOf("Jan", "Feb", "Mar")
    //get을 사용해서 값 사용
    ```
    
# 반복문



