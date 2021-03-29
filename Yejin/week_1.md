# Log와 Logcat
* Log: 코드의 흐름 파악하기 위해 앱 외부에 출력하는 정보
* Logcat: 출력되는 로그를 모아서 보는 도구. 태그를 사용하면 특정 로그만 확인할 수 있음

|함수|의미|내용|
|---|---|-----|
|Log.v()|verbose|상세 로그 내용 출력|
|Log.d()|debug|개발에 필요한 내용 출력(개발자용)|
|Log.i()|information|정보성 일반 메시지 전달|
|Log.w()|warning|경고성 메시지 전달(에러x)|
|Log.e()|error|에러 메시지 출력|

# 변수 var

* 변수선언

```kotlin
var myName="조예진"
```

```kotlin
var myAge : Int
myAge=27 
```

# 상수 val
* 상수선언
```kotlin
val PI=3.141592F
```

```kotlin
val HELLO: String ="안녕"
```

# 조건문 if와 when
* if문 : 범위를 한정할 수 없고 개수가 많을 때 사용
* when문 : 값을 특정할 수 있고 개수가 한정되어 있을 때 사용

> if
* 기본
```kotlin
var ball=4
        if(ball>3){
            Log.d("ControlFlow","4볼로 출루합니다.")
        }
        else{
            Log.d("ControlFlow","타석에서 다음 타구를 기다립니다.")
        }
```

* 변수에 직접 if문 사용하기
```kotlin
var a=5
var b=3
var bigger= if(a>b) a else b
```

* if문 마지막 값을 반환값으로 사용하기
```kotlin
var a=5
var b=3
var bigger= if(a>b){
  a=a-b
  a} //마지막 줄의 a 값이 변수 bigger에 저장된다.
```

> when 
* 기본
```kotlin
var now=10
when (now) {
        8->{
                Log.d("when". "현재 시간은 8시입니다.")
        }
        9->{
                Log.d("when". "현재 시간은 9시입니다.")
        }
        else->{
                Log.d("when". "현재 시간은 9시가 아닙니다.")
        }
}        
```   

* 콤마로 구분해서 사용하기
```kotlin
var now=10
when (now) {
        8, 9->{
                Log.d("when". "현재 시간은 8시 또는 9시입니다.")
        }
        else->{
                Log.d("when". "현재 시간은 9시가 아닙니다.")
        }
}
```

* 범위값을 비교하기
```kotlin
var ageOfMichael=19
when (geOfMichael){
        in 10...19->{
                Log.d("when","마이클은 10대입니다.")
        }
        !in 10...19->{
                Log.d("when","마이클은 10대가 아닙니다.")
        }
        else->{
                Log.d("when","마이클의 나이를 알 수 없습니다.")
        }
}
```

* 파라미터 없는 when 사용하기
```kotlin
var currentTime=6
when {
        currentTime==5->{
                Log.d("when","현재 시간은 5시입니다.")
        }
        currentTime>5->{
                Log.d("when","현재 시간은 5시가 넘었습니다.")
        }
        else->{
                Log.d("when","현재 시간은 5시 이전입니다.")
        }
}
```   

# 배열과 컬렉션
> 배열
* 배열선언
```kotlin
var students=IntArray(10)
var longArray=LongArray(10) //Int, Double과 같은 기본 타입 뒤에 Array를 붙여서 만든다.
```

* 문자 배열에 빈 공간 할당
```kotlin
var stringArray=Array(10,{item->""})
```

* 값으로 배열 공간 할당
```kotlin
var dayArray=arrayOf("MON", "TUE","WED","THU","FRI","SAT","SUN")
```

* 배열에 값 입력하기
```kotlin
student[0]=90
student.set(1,91) // 두 개의 방법이 있다.
```

* 배열에서 값 꺼내기
```kotlin
var seventhValue=intArray[6]
var tenthValue=intArray.get(9) // 두 개의 방법이 있다.
```

> 컬렉션
- 컬렉션=동적 배열
1. 리스트(List): 저장되는 데이터에 인덱스를 부여한 컬렉션. 중복된 값 입력 가능.

-리스트 생성
```kotlin
var list = mutableListOf("MON","TUE","WED")
```

-리스트에 값 추가
```kotlin
mutableList.add("THU") //값이 추가되면서 동적으로 리스트의 공간이 자동으로 증가.
```

-리스트에 입력된 값 사용
```kotlin
var variable = mutableList.get(1)
```

-리스트 값 수정하기
```kotlin
mutableList.set(1,"수정할 값")
```

-리스트에 입력된 값 제거하기
```kotlin
mutableList.removeAt(1) // <- 두번째 값을 제거하면 세번째 값부터 인덱스가 하나씩 자동으로 감소
```

-빈 리스트 사용하기
```kotlin
var stringList = mutableListOf<String>()
```

-컬렉션 개수 가져오기
```kotlin
mutableList.size // 괄호가 없으니 함수가 아니고 '프로퍼티'라고 부른다.
```

2. 셋(Set) : 중복을 허용하지 않는 리스트, 인덱스로 조회할 수 없고 get함수도 없다.

-셋 선언
```kotlin
var set = mutableSetOf<String>()
```

-빈 셋으로 초기화하고 값 입력하기
```kotlin
set = mutableSetOf<String>()
set.add("JAN")
set.add("FEB")
set.add("FEB") //동일한 값은 입력되지 않는다.
```

-셋 사용하기
```kotlin
Log.d("Collection","Set 전체출력 =$(set)")
```

-셋 삭제하기
```kotliset
set.remove("FEB") //리스트는 인덱스를 이용해 삭제하지만, 셋은 값을 직접 조회해서 삭제한다.
```

3. 맵(Map): Key 와 Value 쌍으로 입력되는 컬렉션.
-맵 생성하기
```kotlin
var map= mutableMapOf<String,String>()
```

-값 추가하기
```kotlin
map.put("키1","값1")
map.put("키2","값2")
```

-맵 사용하기
```kotlin
Log.d("CollectionMap","map에 입력된 키1의 값은 &{map.get("키1")입니다."}
```

-맵 수정하기
```kotlin
ㅡmap.put("키2","수정") //키는 유지된 채로 그 값만 변한다.
```

-맵 삭제하기
```kotlin
ㅡmap.remove("키2")
```

>이뮤터블 컬렉션
- 이뮤터블 컬렉션: 크기와 값을 변경할 수 없음.  add, set 함수 지원x. 기존의 컬렉션에서 접두어 mutable만 제거하고 사용.

```kotlin
val IMMUTALE_LIST = listOf("JAN", "FEB", "MAR") //생성
Log.d("Collection", "리스트의 두번째 값은 ${IMMUTALE_LIST.get(1)}입니다.")
```


# 반복문
