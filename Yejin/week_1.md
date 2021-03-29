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

<pre>
<code>
var myName="조예진"
</code>
</pre>

<pre>
<code>
var myAge : Int
myAge=27 
</code>
</pre>

# 상수 val
* 상수선언
<pre>
<code>
val PI=3.141592F
</code>
</pre>

<pre>
<code>
val HELLO: String ="안녕"
</code>
</pre>

# 조건문 if와 when
> if
* 기본
<pre>
<code>
var ball=4
        if(ball>3){
            Log.d("ControlFlow","4볼로 출루합니다.")
        }
        else{
            Log.d("ControlFlow","타석에서 다음 타구를 기다립니다.")
        }
</code>
</pre>

* 변수에 직접 if문 사용하기
<pre>
<code>
var a=5
var b=3
var bigger= if(a>b) a else b
</code>
</pre>

* if문 마지막 값을 반환값으로 사용하기
<pre>
<code>
var a=5
var b=3
var bigger= if(a>b){
  a=a-b
  a} //마지막 줄의 a 값이 변수 bigger에 저장된다.
</code>
</pre>

> when 
* 기본
<pre>
<code>
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
</code>
</pre>     

* 콤마로 구분해서 사용하기
<pre>
<code>
var now=10
when (now) {
        8, 9->{
                Log.d("when". "현재 시간은 8시 또는 9시입니다.")
        }
        else->{
                Log.d("when". "현재 시간은 9시가 아닙니다.")
        }
}
</code>
</pre> 

* 범위값을 비교하기
<pre>
<code>
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
</code>
</pre>

* 파라미터 없는 when 사용하기
<pre>
<code>
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
</code>
</pre>

# 배열과 컬렉션


# 반복문
