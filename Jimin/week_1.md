# Log

|   함수    |  내용  | 
| :-------: | :----: | 
| Log.v() | verbose, 상세 로그 내용 |  
| Log.d() | debug, 개발에 필요한 내용 출력 |
| Log.i() | information, 정보성의 일반적인 메시지 전달|
| Log.w() | warning, 에러는 아니지만 경고성 메시지 전달  |
| Log.e() | error, 실제 에러 메시지 출력 |

```kotlin
//Logcat -> 태그 검색해서 해당 로그만 확인 가능
Log.d("태그","출력 메시지")
```


# 변수 

```kotlin
//변수 선언과 동시에 값 넣기
var myName = "지민이"
//값으로 초기화하지 않고 선언만 하고 사용
var myAge: Int  
myAge = 22
```

- 상수 val  
: 한 번 입력된 값 변경할 수 없음  
: 모두 대문자로 작성  
```kotlin
val PI = 3.141592F
```  

# 조건문

> if-else  
- 변수에 if문 사용  
- ${변수} 사용  

```kotlin
var eraOfRyu = 2.32
var eraOfDegrom = 2.43
var TAG = "MLB_Result"

val era = if (eraOfRyu> eraOfDegrom){
  Log.d(TAG,"2019 류현진이 디그롬을 이겼음")
  eraOfRyu
  } else {
    Log.d(TAG,"2019 디그롬이 류현진을 이겼음")
    eraOfDegrom
  }
Log.d(TAG,"2019 MLB에서 가장 높은 ERA는 ${era}입니다. ")
``` 

![image](https://user-images.githubusercontent.com/50178026/112721929-e60e1800-8f49-11eb-8403-eafe314b0f83.png)  
> when  
- 다른 언어에서의 switch와 유사  

```kotlin
//기본 구조
when(파라미터){
  비교값1 -> {
  }
  비교값2 -> {
  }
  비교값 3 -> {
  }
}
```  
### 비교값 예시  
- 콤마로 구분해서 사용
```kotlin
when(now){
  8,9 -> {
    Log.d("when","현재 시간은 8시 혹은 9시")
  }
  else -> {
    Log.d("when","현재 시간은 8,9시가 아님")
  }
}
```
- 범위 값 비교 
```kotlin
when(age){
  in 10..19 -> {
    Log.d("when","10대임")
  }
  !in 10..19 -> {
    Log.d("when","10대 ")
  }
}
```
- 파라미터 생략 가능

# 배열과 컬렉션  

> 배열 
- 배열 선언
```kotlin
// var 변수 = Array(개수)
// 기본 타입 뒤에 Array 붙여서 사용  
var students = IntArray(10)
var longArray = LongArray(10)
var CharArray = CharArray(10)
var FloatArray = FloatArray(10)
var DoubleArray = DoubleArray(10)
//String은 기본 타입이 아니기 때문에 빈 공간 할당해서 사용
var stringArray = Array(10,{item->""})
//arrayOf 함수 이용해 직접 할당 가능
var dayArray = arrayOf("MON","TUE","WED","THU","FRI","SAT","SUN")
```  
- 배열에 값 입력
```kotlin
배열명[인덱스]=값
배열명.set(인덱스,값)
```
- 배열에 있는 값 꺼내기
```kotlin
배열명[인덱스]
배열명.get(인덱스)
```
> 컬렉션
: 동적 배열

- List
```kotlin
//mutable"type"Of 로 생성  
//빈 컬렉션 : var list = mutableListOf<String>() 
var list = mutableListOf("MON","TUE","WED")
//입력되는 순서대로 인덱스 지정
list.add("THU")
//인덱스 값 변수에 지정
var variable =list.get(1)
//수정하기
list.set(1,"수정할 값")
//제거
//아래의 경우 두 번째 값 삭제, 세 번째 값부터 인덱스 감소하면서 빈자리의 인덱스로 이동  
list.removeAt(1)
//컬렉션 개수 가져옴
mutableList.size
```
- Set 
: 중복을 허용하지 않는 리스트  
: 인덱스 지원하지 않음
```kotlin  
var set = mutableSetOf<String>()  
set.add("JAN")  
set.add("FEB")  
set.add("JAN") // 동일 값 입력되지 않음  
//값이 중복되지 않으므로 값으로 삭제 가능  
set.remove("FEB")
```  

- Map
: key, value의 쌍으로 입력
```kotlin
var map = mutableMapOf<String,String>()
map.put("key1","value1")
map.put("key2","value2")
map.put("key3","value3")
//값 얻음
map.get("key1")
//동일한 키를 가진 값이 있으면 키는 유지, 그 값만 수정
map.put("key2","수정")
//키를 입력해서 값 삭제
map.remove("key2")
```

> Immutable Collection  
: 크기, 값 변경 불가  
```kotlin
//여러 개의 값을 중간에 수정하지 않고 사용할 필요 있을 때 사용  
val DAY_LIST = listOf("월","화","수","목","금","토","일")    
```

# 반복문

> for
```kotlin
// 1~10 출력
for (index in 1..10){
  Log.d("index", "현재 숫자는 ${index}")
}
// 0~9 출력
for (index in 0 until 10){
  Log.d("index", "현재 숫자는 ${index}")
}
//0~100 3씩 증가하면서 반복
for (index in 0..100 step 3){
  Log.d("index", "현재 숫자는 ${index}")
}
//100~10 감소
for (index in 100 downTo 10){
  Log.d("index", "현재 숫자는 ${index}")
}
//배열, 컬렉션 이용
var arrayMonth = arrayOf("JAN","FEB","MAR")
for (month in arrayMonth){
  Log.d("for","현재 월은 ${month}")
}
```

> while
```kotlin
//do while 경우 조건 상관없이 일단 한번 실행됨 

//while 문
var game =6 
val match =6
while(game < match){
  Lod.d("while", "while 테스트")
  game+=1
}

//do - while 문
do {
  Log.d("while","do ~ while 테스트")
  game+=1
} while(game<match)

```
> 반복문 제어

- break: 반복문 탈출
- continue: 다음 반복문으로
