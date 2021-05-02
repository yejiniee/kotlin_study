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

### Intent

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

### 새 액티비티 만들고 실행하기

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

### 액티비티 사이에 값 주고받기

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

----

### 액티비티 생명 주기

메서드 | 액티비티 상태 | 설명
----- | --------------|----
onCreate()|만들어짐|액티비티가 생성됨
onStart()|화면에 나타남|화면에 액티비티가 보이기 시작
onResume()|실행중,화면에 나타남|액티비티가 실행되고 있다.(실행중)
onPause()|화면이 가려짐|액티비티 화면의 일부가 다른 액티비티에 가려짐
onStop()|화면이 없어짐|다른 액티비티가 실행되어 화면이 완전히 가려짐
onDestroy()|종료됨|종료됨

* 액티비티 상태변화를 말함.
* 이 메서드들은 override를 통해서 사용
* super.on~() 로 상속받아 사용. 상속받지 않으면 정상적으로 동작하지 않는다.


### 생명주기 콜백

* 액티비티 생성후 화면에 출력 : onCreate - onStart - onResume
* 액티비티를 화면에서 제거 : onPause - onStop(동시에) - onDestroy
* 새 액티비티 생성시 : 현재 액티비티 - onPause - onStop(종료x), 새 액티비티 - onStart - onResume
* 새 액티비티가 현재 액티비티를 모두 가리지 않고 생성될 때 : 현재 액티비티 - onPause - 새 액티비티 종료 - onResume

### 액티비티 백스택

* 액티비티 또는 화면 컴포넌트를 담는 안드로이드의 저장공간
* 액티비티를 후입선출로 담는 스택이라고 생각하자.

### Task와 Process

* Task : Process를 관리하는 작업 단위
* Process : Application의 실행 단위
* Task는 다른 프로세스의 액티비티를 함께 담을 수 있다. = 서로 다른 어플리케이션의 액티비티 공유가능.

### Task관리하기

* Manifest로 관리 : Task와 BackStack으로 관리되는 액티비티는 AndroidManifest.xml의 <activity> 태그 안에 속성처럼 사용가능
  `<activity android:name=".MainActivity" android:launchMode="singleInstance"></activity>`
  
속성 | 설명
-----|-----
launchMode|호출할 액티비티를 생성할 것인지 재사용할 것인지 결정. 디폴트는 새로생성. standard, singleTop,singleTask, singleInstance
taskAffinity|affinity가 동일한 액티비티들은 같은 task에 들어간다. 디폴트는 manifest에 정의된 패키지명->기본적으로 한 앱의 모든 액티비티는 동일한 affinity를 가진다.
allowTaskReparenting|기본값은 false, true일 경우 호출한 액티비티를 동일한 affinity를 가진 태스크에 쌓이도록 한다.
clearTaskOnLaunch|True이면 액티비티 재실행시 메인 액티비티를 제외하고 모두 제거. 기본값 false
alwaysRetainTaskState|기본값은 false, 사용자가 특정 시간동안 앱을 사용하지 않을 경우, 시스템이 Root액티비티를 제외한 액티비티제거. true일 경우 시스템이 관여안함
finishOnTaskLaunch|앱을 다시 사용할 때 이 옵션이 true인 액티비티가 있다면 해당 태스크 종료
  
* startActivity에 전달하는 intent의 flag값으로 관리
  ```kotlin
  val intent = Intent(this, SubActivity::class.java)
  intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
  ```
  + FLAG_ACTIVITY_ 를 접두사로 CLEAR_TOP, NEW_TASK, MULTIPLE_TASK, SINGLE_TOP등이 있다.

-----

## 컨테이너: 목록 만들기

* 위젯의 위치 : 레이아웃사용
* 위젯이나 레이아웃에 데이터를 동적으로 표현 : 컨테이너 사용
* 대표 : RecyclerView
* 컨테이너는 내부 요소의 위치를 결정할 수 있는 속성이 없으므로 컨테이너 안에 레이아웃을 삽입해서 사용

### 스피너
* 리사이클러뷰의 축소버전
* 여러 개의 목록 중 하나를 선택할 수 있는 선택 도구
* Adapter(연결도구)를 사용해 화면에 나타낼 데이터와 화면에 보여주는 스피너를 연결

![image](https://user-images.githubusercontent.com/27190776/116779236-0f254980-aab0-11eb-941e-96b9527b528b.png)

----

### 리사이클러뷰
* 스피너의 확장된 형태
* 레이아웃 매니저를 이용해 리스트를 그리드로 바꿀 수도 있음
* 표시될 데이터와 아이템 레이아웃을 어댑터에서 연결해준다. 어떤 아이템 레이아웃을 사용하느냐에 따라 모양이 다르게 만들 수 있다.

![image](https://user-images.githubusercontent.com/27190776/116779878-e99a3f00-aab3-11eb-9736-720ceefc5828.png)

#### 어댑터 정의
* 리사이클러뷰는 리사이클러뷰어대버라는 메서드 어댑터를 사용해서 데이터 연결. 상속이 필요
```kotlin
//뷰홀더 클래스를 제네릭으로 지정해야하므로, 뷰홀더 클래스를 먼저 생성하자.
//뷰홀더 클래스
//뷰홀더는 화면에 보여지는 개수만큼한 생성되고 목록이 위쪽으로 스크롤될 경우 가장 위의 뷰홀더를 아래에서 재사용한 후 데이터만 바꿔줌.
class 홀더(바인딩): RecyclerView.ViewHolder(바인딩.root) {  //뷰홀더클래스의 생성자에는 다음에 만들 어댑터의 아이템 레이아웃을 넘겨
                                                           //줘야하므로 클래스 생성시 생성자에게서 레이아웃의 바인딩을 넘겨받아야 한다.

}
//어댑터 클래스
class 커스텀어댑터: RecyclerView.Adapter<뷰홀더> {
  ...
  override fun onBindViewHolder(뷰홀더, 아이템 위치) {
  }
}
```

![image](https://user-images.githubusercontent.com/27190776/116780575-95de2480-aab8-11eb-9aa7-9c61c7c6f85e.png)

#### MainActivity.kt에서 어댑터 사용하기

![image](https://user-images.githubusercontent.com/27190776/116780693-3cc2c080-aab9-11eb-9891-147169310eac.png)

#### 레이아웃 매니저 종류

1. LinearLayoutManager
  * 세로 스크롤 : 한줄로 목록 생성
    `LinearLayoutManager(this)`
  * 가로 스크롤 : 칼럼 개수를 정해서 그리드 형태로 목록 생성, 두번째 파라미터 = 가로 스크롤 옵션.
    `LinearLayoutManager(this, LinearLayoutManager.HORIZAONTAL, fale)`

2. GridLayoutManager
  * 데이터의 사이즈에 따라 그리드의 크기가 결정. 두번째 파라미터 = 한 줄에 몇개의 아이템을 표시할 건지 갯수
    `GridLayoutManager(this, 3)`

3. StaggeredGridLayoutManager
  * 세로 스크롤 : 컨텍스트를 사용하지 않음. 첫번째 파라미터 = 한 줄에 표시되는 아이템의 개수, 두번째 파라미터 = 세로 방향 설정
    `StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.VERTICAL)`
  * 가로 스크롤 :
    `StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.HORIZONTAL)`
    
#### 목록 이벤트 처리

* 목록에서 아이템 1개가 클릭되었을 때 처리하는 방법

![image](https://user-images.githubusercontent.com/27190776/116780979-df2f7380-aaba-11eb-9ec2-994b6329d564.png)

* 모든 뷰는 컨텍스트를 가지고 있다. binding.root또한 뷰이기 때문에 binding.root.context형태로 사용가능
----

## Fragment

* 화면을 분할해서 독립적인 코드로 구성할 수 있게 도와줌
* 화면(뷰)이 하나만 필요할 때는 프래그먼트 사용X, 프래그먼트도 하나의 모듈로써 동작한다.

### Fragment 액티비티에 추가하기

* build.gradle에 viewBinding설정

#### List Fragment 만들기
* Fragment는 하나의 뷰로 동작하기 때문에 액티비티안에 뷰를 삽입할 수 있는 레이아웃을 준비해야한다

![image](https://user-images.githubusercontent.com/27190776/116806944-46a4fc00-ab6b-11eb-92aa-b9295d112608.png)

#### 액티비티에 Fragment추가
* 액티비티에 프래그먼트를 삽입하기 위해서는 프래그먼트 매니저를 통해 삽입할 레이아웃의 id를 지정.
* 프래그먼트 삽입과정은 하나의 트랜잭션으로 관리되기 때문에 트랜잭션 매니저를 통해 begin transaction > add fragment > commit transaction 순서로 처리됨
* 트랜잭선 : 여러 개의 의존성 동작을 한 번에 실행시, 중간에 하나라도 잘못되면 모든 동작을 복구하는 작업단위

![image](https://user-images.githubusercontent.com/27190776/116806927-2bd28780-ab6b-11eb-83e5-5fafa06f99c2.png)

#### 레이아웃에서 Fragment 추가하기

* fragment컨테이너를 사용해 레이아웃 파일에서 위젯처럼 프래그먼트 추가.

![image](https://user-images.githubusercontent.com/27190776/116807200-ce3f3a80-ab6c-11eb-9783-6fa117ed103b.png)

----

### Fragment 화면 전환

#### 상세프래그먼트 만들기
* New - Fragment - Fragment(Blank) - 이름 DetailFragment로 수정

![image](https://user-images.githubusercontent.com/27190776/116807360-c633ca80-ab6d-11eb-956b-d0a1023b6023.png)

#### 메인 액티비티에 두 프래그먼트 연결
* 프래그먼트를 메인 액티비티에서 생서하고, 프래그먼트를 담는 레이아웃도 메인 액티비티에 있으므로 화면전환을 위한 코드는 메인 액티비티에 작성

![image](https://user-images.githubusercontent.com/27190776/116807645-4444a100-ab6f-11eb-853e-0b7555164e23.png)


#### ListFragment.kt 코드 수정
* onAttach()를 통해 코드를 전달 받음

![image](https://user-images.githubusercontent.com/27190776/116808201-799ebe00-ab72-11eb-8075-9fdf95e7b961.png)

+ flase 를 false로 고쳐도 안됨.

![image](https://user-images.githubusercontent.com/27190776/116808382-56c0d980-ab73-11eb-8b60-514e24a4069b.png)

----

### 프래그먼트로 값 전달하기

* 프래그먼트 생성시 값 전달
* 이미 생성되어 있는 프래그먼트에 값 전달

#### 프래그먼트 생성시 값 전달
* arguments 이용.

![image](https://user-images.githubusercontent.com/27190776/116809730-7c9dac80-ab7a-11eb-9930-f03350e76884.png)

![image](https://user-images.githubusercontent.com/27190776/116809739-88896e80-ab7a-11eb-992e-61b9fc72fdc0.png)


#### 생성된(화면에 보이는) 프래그먼트에 값 전달하기

