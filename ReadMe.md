# ADS04 Android

## 수업 내용

- DI 학습
- 관련 library 학습

## Code Review


### MainActivity
```Java
@Fullscreen
@EActivity(R.layout.activity_main)
@WindowFeature(Window.FEATURE_NO_TITLE)
public class MainActivity extends AppCompatActivity {


    @ViewById
    TextView text;

    @AfterViews
    public void init(){
        text.setText("Hello AA");
        run();
    }

    @Background
    public void run(){
        // 여기는 sub thread에서 실행된다
        for(int i =0; i<10; i++){
            main(i);

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    @UiThread
    public void main(int i ){
        //여기 코드는 main thread 실행됨
        text.setText(i+"");
    }


//        //di 사용
//        ButterKnife.bind(this);
//       text.setText("hello android");
//        // di 미사용
//        text = (TextView) findViewById(R.id.text);



}
```


## 보충설명

### Dependency 는 무엇?

- Dependency (또는 의존성)는 코드에서 두 모듈간의 연결이라고 볼 수 있다. 객체지향언어에서는 두 클래스간의 관계라고도 말한다. 일반적으로 둘 중 하나가 다른 하나를 어떤 용도를 위해 사용한다.

### 왜 Dependency는 위험할까?

- 하나의 모듈이 바뀌면 의존한 다른 모듈까지 변경이 이루어지기 때문이다. 그리고 테스트 가능한 애플리케이션을 만들고자 할 때 의존성이 있으면 유닛테스트 작성이 어려운데 유닛테스트의 목적 자체가 다른 모듈로부터 독립적으로 테스트하는 것을 요구하기 때문이다.

### Dependency Injection이란

![dependency Injection](http://cfile26.uf.tistory.com/image/2319B83758E27BE11EEB8B)

- 의존성 주입(Dependency Injection, DI)은 프로그래밍에서 구성요소간의 의존 관계가 소스코드 내부가 아닌 외부의 설정파일 등을 통해 정의되게 하는 디자인 패턴 중의 하나이다
- Dependency Injection이란 바로 이런 문제점에서 시작해서 모듈간의 의존성을 관리해주고 비즈니스 로직과 관련없지만 꼭 필요한 보일러플레이트 코드를 줄여주는 것을 의미한다.

#### Dependency Injection 이점

- 의존 관계 설정이 컴파일시가 아닌 실행시에 이루어져 모듈들간의 결합도 를 낮출 수 있다.
- 코드 재사용을 높여서 작성된 모듈을 여러 곳에서 소스코드의 수정 없이 사용할 수 있다.
- 모의 객체 등을 이용한 단위 테스트의 편의성을 높여준다.

#### 적용 유형

``` HTML
마틴 파울러는 다음과 같은 세 가지의 의존성 주입 패턴을 제시하였다.
생성자 주입 : 필요한 의존성을 모두 포함하는 클래스의 생성자를 만들고 그 생성자를 통해 의존성을 주입한다.
세터(Setter)를 통한 주입 : 의존성을 입력받는 세터(Setter) 메소드를 만들고 이를 통해 의존성을 주입한다.
인터페이스(Interface)를 통한 주입 : 의존성을 주입하는 함수를 포함한 인터페이스를 작성하고 이 인터페이스를 구현하도록 함으로써 실행시에 이를 통하여 의존성을 주입한다.
```
### AndroidAnnotations

- View, Extras, System Service, Resource 에 대한 의존성 주입을 Annotation으로 편리하게 지원하는 Library
- 명확한 의도와 간단한 코드가 그 목표를 달성하는 가장 좋은 방법이라는 것을 목표로 하고 있음.

#### 사용법

- 상기 code review 참고

### Butter Knife Library

- View, Resource 에 대한 의존성 주입을 Annotation으로 편리하게 지원하는 Library.

#### 사용법

1. @BindView 주석(annotation)을 이용해서 findViewById를 제거
2. 여러 개의 뷰와 배열을 그룹화할 수 있음
3. 리스너를 위한 익명의 내부 클래스들을 @OnClick annotation을 이용해서 제거
4. resource annotation을 이용해서 resource 검색작업을 없앨 수있음.

```Java
class ExampleActivity extends Activity {
  @BindView(R.id.user) EditText username;
  @BindView(R.id.pass) EditText password;

  @BindString(R.string.login_error) String loginErrorMessage;

  @OnClick(R.id.submit) void submit() {
    // TODO call server...
  }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.simple_activity);
    ButterKnife.bind(this);
    // TODO Use fields...
  }
}

```


- 참고하면 좋은 블로그 : http://d2.naver.com/helloworld/342818


### 출처

- 출처: http://imcreator.tistory.com/106 [인문과 공학의 사이 어느 중간쯤]
- 출처: http://selfbrandmaking.tistory.com/1 [MAKING OWN BRAND]


## TODO

- DI, CI, AOP의 개념 공부해보기
- DAGGER2 Library도 사용해보기

## Retrospect

- 프로그래밍하면서 불편하다거나 중복된 코드를 보면서 당연하다고 생각했는데, 이러한 라이브러리들을 보니 당연한 것이 결코 당연하다고만 여길 필요가 없다라는 생각을 했다.
- 굉장히 직관적이기에 본인도, 다른 사람들도 코드 읽기 수월할 것 같다.
- 프로그래머는 비효율적인 것에 대해 깊은 고민을 해야하는 직업이라는 생각을 했다. 


## Output
- 생략