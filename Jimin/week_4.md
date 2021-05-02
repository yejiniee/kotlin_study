# Activity
: 사용자가 직접 보고 입력하는 화면을 담당하는 컴포넌트

## Context
- 시스템을 사용하기 위한 정보와 도구가 담겨 있는 클래스
- 대부분 context는 컴포넌트 실행시 함께 생성, 생성된 컴포넌트가 가지고 있는 메서드를 호출해 각각의 도구 사용할 수 있음
- Application Context
  - 애플리케이션과 관련된 핵심 기능 담고 있는 클래스
  - 하나의 인스턴스만 생성됨
  - 호출하는 지점과 관계없이 동일한 컨텍스트 호출됨
- Base Context
  - 4대 컴포넌트 -> activity, service, content provider, broadcast receiver의 기반 클래스
  - 컴포넌트 개수만큼 컨텍스트 함께 생성 -> 호출되는 지점에 따라 다른 컨텍스트 호출

## Intent

- 실행할 대상의 액티비티 이름과 전달할 데이터를 담아서 인텐트 생성
- 생성한 인텐트를 startActivity() 메서드에 담아서 호출 -> 액티비티 매니저에 전달
- 액티비티 매니저는 인텐트 분석해, 지정한 액티비티를 실행시킴
- 전달된 인텐트 -> 타깃 액티비티에 전달
- 타깃 액티비티에서는 전달받은 인텐트에 데이터가 있다면 이를 꺼내서 사용

### Main activity에서 Sub activity 실행

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        binding.button.setOnClickListener{ startActivity(intent)}

    }
}
```

### 액티비티 사이 값 주고 받기

> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        // 키, 값 조합으로 번들에 직접 넣음, 꺼낼 때는 키 이용해서 꺼냄
        intent.putExtra("from1","hello bundle")
        intent.putExtra("from2", 2021)
        binding.button.setOnClickListener{ startActivity(intent)}

    }
}
```
> SubActivity.kt
```kotlin
class SubActivity : AppCompatActivity() {

    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)
        
        // intent 이용, key를 통해서 값 받음
        binding.to1.text = intent.getStringExtra("from1")
        // text는 문자열만 받을 수 있기 때문에 "" 감싸고 문자열 템플릿을 사용해서 문자열로 변환
        binding.to2.text = "${intent.getIntExtra("from2",0)}"
    }
}
```

### 메인 액티비티에서 값 돌려받기
> MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent = Intent(this, SubActivity::class.java)
        intent.putExtra("from1","hello bundle")
        intent.putExtra("from2", 2021)
        
        //값 돌려받기 위해서 startActivityForResult(Intent, requestCode) 사용 
        binding.button.setOnClickListener{ startActivityForResult(intent,99)}
    }
    
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (resultCode == Activity.RESULT_OK){
            when(requestCode) {
                99 -> {
                    val message = data?.getStringExtra("returnValue")
                    Toast.makeText(this, message, Toast.LENGTH_LONG).show()
                }
            }
        }
    }
}
```

> SubActivity.kt
```kotlin
class SubActivity : AppCompatActivity() {

    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        binding.to1.text = intent.getStringExtra("from1")
        binding.to2.text = "${intent.getIntExtra("from2",0)}"


        binding.button2.setOnClickListener{
            val returnIntent = Intent()
            //입력된 문자열 intent에 put
            returnIntent.putExtra("returnValue",binding.editText.text.toString())
            
            //setResult(상태값, 인텐트)
            setResult(Activity.RESULT_OK,returnIntent)
            finish()
        }
    }
}
```

## 생명 주기

|메서드|액티비티 상태|설명|
|------|---|---|
|OnCreate()|만들어짐|액티비티 실행됨|
|OnStart()|화면에 나타남|화면에 보이기 시작|
|OnResume()|현재 실행 중|실제 액티비티가 실행 중|
|OnPause()|화면 가려짐|액티비티 일부가 다른 액티비티에 가려짐|
|OnStop()|화면 없어짐|다른 액티비티가 실행되어서 화면이 완전히 가려짐|
|OnDestroy()|종료됨|액티비티가 종료됨|
