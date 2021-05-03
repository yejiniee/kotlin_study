# 액티비티
## 인텐트
액티비티를 실행하기 위해선 기본적으로 인텐트가 필요하다.

*액티비티 전환하기

패키지명 우클릭->[New]->[Activity]->[Empty Activity]->서브 액티비티 생성

```kotlin
class MainActivity : AppCompatActivity() {
    val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        val intent= Intent(this, SubActivity::class.java)
        binding.btnStart.setOnClickListener{startActivity(intent)} //btnStart는 버튼의 id이다.
    }
}
```

*액티비티 사이에 값 주고받기
```kotlin
class SubActivity : AppCompatActivity() {
    val binding by lazy { ActivitySubBinding.inflate(layoutInflater) }
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        binding.to1.text=intent.getStringExtra("from1")
        binding.to2.text="${intent.getIntExtra("from2",0)}" //텍스트뷰의 text 속성은 문자열만 받을 수 있기 때문에 ${}을 사용해 문자열로 바꿔줌

    }
}

```

