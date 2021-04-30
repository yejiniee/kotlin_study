# 화면 구성하기

* 컴포넌트
* 액티비티와 컨테이너, 프래그먼트
* 컨텍스트
* View 클래스, 커스텀 위젯
* ViewPager와 TabLayout
--------------------------

> 컴포넌트
* Activity : 화면 UI를 담당하는 컴포넌트
* Broadcast Receiver : 시스템 또는 사용자가 발생하는 메시지를 수신하는 컴포넌트
* Service : 백그라운드 코드 처리를 담당하는 컴포넌트(화면이 없는 Activity라고 생각)
* Content Provider : 앱끼리의 데이터 공유를 위한 컴포넌트

> 컴포넌트를 사용하기 위한 도구
* Intent : 액티비티, 브로드캐스트 리시버, 서비스를 실행하기 위해 시스템에 전달되는 메시지 도구
* Content Resolver : Content Provider가 제공하는 데이터를 사용하기 위한 도구

## 액티비티

* 사용자가 직접 보고 입력하는 화면을 담당하는 컴포넌트
* 액티비티는 컨텍스트를 상속받아 구현된다.

### Context

* 컴포넌트와 화면 요소들을 사용하기위해 필요
* 시스템을 사용하기 위한 정보(프로퍼티)와 도구(메서드)가 담겨 있는 클래스
* 컴포넌트 실행시 함께 생성

> 컨텍스트 종류
  * Application Context : 애플리케이션 관련 핵심기능을 담고 있는 클래스. 앱을 통틀어서 하나의 인스턴스만 생성된다=호출 지점과 관계없이 동일한 컨텍스트 호출. applicationContext를 호출해서 사용.
  * Base Context : 액티비티, 서비스, 컨텐트 프로바이더, 브로드캐스트 리시버의 기반 클래스. baseContext 또는 this로 컨텍스트 사용. 컴포넌트 개수만큼 컨텍스트 생성=호출시 마다 다른 컨텍스트 호출.

----

## Intent

* 액티비티를 실행하기 위해서, 컨텍스트가 제공하는 메서드를 호출해야하는데, 이때 실행할 액티비티가 명시된 인텐트를 해당 메서드에 전달해야한다.
* 개발자가 어떤 의도를 가지고 메서드를 실행할 것인지를 인텐트에 담아 안드로이드에 전달
* 액티비티를 실행하려면 인텐트가 필요하지만, MainActivity는 자동으로 등록되고 실행된다.
* MainActivity외에 다른 액티비티를 사용할 때는 인텐트에 새 액티비티의 이름을 담아서 시스템에 전달.
  
* 전달과정
  1. 실행 대상의 액티비티 이름과 전달할 데이터를 담아서 인텐트 생성
  2. 생성한 인텐트를 startActivity() 메서드에 담아서 호출하면 액티비티 매니저에 전달
  3. 액티비티 매니저는 인텐트 분석 -> 액티비티 실행
  4. 전달된 인텐트는 타깃 액티비티로 전달
  5. 타깃 액티비티에서는 전달받은 인텐트에 데이터가 있다면 이것을 꺼내서 사용할 수 있다.

----

## 새 액티비티 만들고 실행하기

* app - java 밑에 있는 패키지에서 마우스 우클릭하여 New - Activity - Empty Activity
* SubActivity 생성(xml파일은 activity_sub.xml), Launcher Activity는 프로그램실행시 먼저 호출되도록 설정하는 것
  
* 메인 액티비티에서 서브 액티비티 실행하기
```kotlin
//build.gradle 파일에 viewBinding설정을 한 후,
class MainActivity: AppCompatActivity() {
  val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }
  
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(binding.root)
    //setContentView아래에 작성해 인텐트 생성. 인텐트 사용을 위한 작성규칙
    val intent = Intent(this, SubActivity::class.java)
    //btnStart는 SubActivity를 실행시키는 버튼의 id
    binding.btnStart.setOnClickListener{ startActivity(intent) }
  }
}
```

----

## 액티비티 사이에 값 주고받기

* 인텐트 내부의 bundle 이라는 데이터 저장공간에 데이터를 담아 주고받을 수 있다.
* 인텐트에 값 입력시 : 키와 값의 조합으로 번들에 넣는다.
* 인텐트에서 값 꺼낼시 : 키로 꺼낸다.
  
* val intent = ... 와 binding.btnStart... 사이에 putExtra()메서드를 사용해서 인텐트에 값을 전달하는 코드 추가
* putExtra(키, 값)
* 전달받을 값을 출력할 뷰를 배치
* SubActivity.kt

> 메인->서브액티비티로 값 전달

```kotlin
class SubActivity: AppCompatActivity() {
  val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(binding.root)
    //setContentView아래에 추가. 인텐트에 담겨온 값을 꺼내는 getStringExtra()사용. value에 따라 함수를 다르게 사용
    binding.textid1.text = intent.getStringExtra("키")
    //getIntExtra의 두번째 파라미터는 디폴트로 사용할 값. "${ }" 는 문자열로 변환하는 템플릿
    binding.textid2.text = "${intent.getIntExtra("키2", 0)}"
  }
}
```

> 서브->메인액티비티로 값 돌려받기

* activity_sub.xml에 뷰 배치
* 서브 액티비티가 종료될 때 자신을 호출했던 액티비티로 값을 돌려주는 코드 추가
* SubActivity.kt 의 onCreate메서드 안에 'btnClose' = button의 id값, 입력 후 클릭리스너를 단다. 

```kotlin

binding.btnClose.setOnClickListener {
  //호출한 메인 액티비티에 돌려줄 인텐트 하나 생성 후 변수에 저장. 돌려줄 때는 대상을 지정하지 않아도 되므로 Intent에 아무것도 담지 않는다.
  val returnIntent = Intent()
  //editMessage란 id값을 가지는 위젯의 text속성을 string타입으로 반환
  returnIntent.putExtra("returnValue", binding.editMessage.text.toString())
  //setResult : 호출한 측으로 상태값과 returnIntent전달. 상태값은 RESULT_OK, RESULT_CANCLED 이다.
  setResult(RESULT_OK, returnIntent)
  //서브액티비티 종료
  finish()
}
```

* MainActivity.kt 안에 SubActivity에서 돌려준 값을 받는 코드 추가. onCreate()메서드 밖을 클릭후 ctrl+O 누른다.(혹은 우클릭 - Generate - Override Methods)
* 메서드 목록 중 onActivityResult를 선택하고 ok
```kotlin
//requestCode: 호출 시 startActivityForResult 메서드에 인텐트와 함께 입력해서 호출한 코드 구분.
//resultCode: 결과 처리후 서브 액티비티에서 입력하는 코드. RESULT_OK를 담아 보낸다.
//data: 결과 처리 후 서브 액티비티가 넘겨주는 인텐트
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
  super.onActivityResult(requestCode, resultCode, data)
  //resultCode가 정상인지 체크
  if(resultCode == RESULT_OK) {
    //정상이라면 인텐트 값을 변수에 저장
    val message = data?.getStringExtra("returnValue")
    //해당 메시지를 화면에 잠깐 나타났다 사라지도록 출력. .show()를 해야만 화면에 나타난다
    //첫번째 파라미터, 화면을 위한 기본 도구인 컨텍스트. 액티비티가 이미 갖고있으므로 this
    //두번째 파라미터, 출력될 메시지를 문자열로 전달
    //세번째 파라미터, 메시지의 출력시간. LENGTH_LONG, LENGTH_SHORT
    Toast.makeText(this, message, Toast.LENGTH_LONG).show()
  }
}
```
* 메인 액티비티에서 서브 액티비티를 호출한 후 값을 돌려 받고 싶을 때는 startActivityForResult() 메서드 사용
* bindingbtnStart.setOnClickListener { startActivity(intent) 를 startActivityForResult(intent, 99) } 로 변경 (두번째 파라미터는 requestCode로 구분하기위함)
* onActivityResult 메서드 안에 작성한 코드에 when문을 추가해서 requestCode가 요청코드와 같은 99인지 체크
```kotlin
if (resultCode == RESULT_OK) {
  when (requestCode) {
    99 -> {
      val message = data?.getStringExtra("returnValue")
      Toast.makeText(this, message, Toast.LENGTH_LONG).show()
    }
  }
}
```

