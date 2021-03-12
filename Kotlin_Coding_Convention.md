# Kotlin Coding Conventions

Kotlin 공식 문서의 Coding Convention을 따름<br/>
https://kotlinlang.org/docs/coding-conventions.html#colon

## 1. Source Code Organization

### 디렉토리 구조
코틀린과 자바를 같이 사용하는 프로젝트에서 kotlin 소스 파일은 Java 소스 파일과 동일한 소스 루트 및 동일한 디렉토리 구조<br/>
순수 코틀린 프로젝트에서 권장되는 디렉토리 구조는 공통 루트 패키지가 생략된 패키지 구조를 따름

### 소스 파일 이름
- 클래스 이름과 동일
- `.kt` 확장자
- 첫 글자가 대문자인 Camel Case

### 소스 파일 구성
하나의 소스 파일에 여러 선언을 배치하는 것은 서로 연관되어 있고 파일 크기가 적절한 수준으로 유지되는 조건에 한해서 권장<br/>
클래스의 모든 클라이언트와 관련된 스에 대한 확장 기능을 정의할 때는 클래스 자체가 정의된 동일한 파일에 배치

### 클래스 레이아웃
클래스의 내용은 아래 순서로 정렬
1. 속성 선언 및 초기화 블록
2. 보조 생성자
3. 메소드 선언
4. 동반자 객체

- 메소드 선언을 사전순 또는 가시성에 따라 정렬하지 않을 것
- 일반 메서드와 확장 메소드를 분리하지 않을 것
- 연관될 항목을 모아서 위에서 아래로 논리를 따라갈 수 있도록 할 것

중첩 클래스를 해당 클래스를 사용하는 코드 옆에 넣을 것

### 인터페이스 구현 레이아웃
구현 멤버를 인터페이스 멤버와 동일한 순서로 유지

## 2. Naming Rules
`Kotlin`은 `Java`의 네이밍 규칙을 따름

패키지 이름은 소문자이며 `_`는 사용하지 않음<br/>
여러 단어로 된 이름은 권장되지 않지만 사용할 경우 Camel Case 적용<br/>
클래스와 객체의 이름은 대문자로 시작하고 Camel Case 사용<br/>

```Kotlin
open class DeclarationProcessor { /*...*/ }
object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
```

### 함수 네이밍
함수 속성 및 지역 변수의 이름은 소문자로 시작하는 Camel Case, `_`는 사용하지 않음<br/>

```Kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

**예외)** 클래스의 인스턴스를 생성하는데 사용되는 팩토리 함수는 생성되는 클래스와 동일한 이름을 가질 수 있음

```Kotlin
interface Foo { /*...*/ }
class FooImpl : Foo { /*...*/ }
fun Foo(): Foo { return FooImpl() }
```

### 테스트 메소드 네이밍
테스트에서만 ```으로 둘러싸서 공백 사용 허용 (Android 런타임에서 지원하지 않음)<br/>
`_`도 테스트 코드에서 사용 가능

```Kotlin
class MyTestCase {
     @Test fun `ensure everything works`() { /*...*/ }
     
     @Test fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

### 속성 네이밍
상수의 이름은 밑줄로 분리되는 대문자 사용

```Kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```

행동(behavior) 또는 상수를 가지는 최상위(top-level) 또는 object 속성의 이름은 Camel Case 사용

```Kotlin
val mutableCollection: MutableSet<String> = HashSet()
```

singleton 객체에 대한 참조를 가지는 속성의 이름은 object 선언과 동일한 스타일을 사용할 수 있음

```Kotlin
val PersonComparator: Comparator<Person> = /*...*/
```

열거형 상수의 경우 밑줄로 구분되는 대문자 또는 대문자로 시작하는 Camel Case 사용

### 후위 속성(backing properties) 네이밍
클래스에 개념적으로는 동일하지만 하나는 public API의 일부이고 다른 하나는 상세 구현으로 `private`일 경우 `private` 속성의 접두사에 `_` 사용

```Kotlin
class C {
    private val _elementList = mutableListOf<Element>()

    val elementList: List<Element>
         get() = _elementList
}
```

### Good Names
- 클래스의 이름은 보통은 명사 또는 명사구 (클래스를 설명할 수 있는)
- 메소드의 이름은 일반적으로 동사 또는 메소드의 행위를 나타내는 동사 구문
- 의미없는 단어를 사용하지 않음
- 약어를 이름의 일부로 사용하는 경우, 약어가 두 개의 문자로 구성되면 대문자로 시작
- 약어가 두 문자 이상으로 길면, 첫글자만 대문자

## 3. Formatting

indentation 4칸, tab 사용 금지

중괄호는 문장 행의 끝에 여는 괄호를 사용, 닫는 괄호는 별도의 라인에 여는 괄호와 열을 맞춰 사용

```Kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```

Kotlin에서 `;`은 선택사항이므로 줄바꿈이 중요<br/>
언어의 디자인이 Java 스타일을 따르기 때문에 다른 스타일을 사용하면 다른 결과가 생길 수 있음

### 공백
- 이항 연산자 앞 뒤에 공백 사용 **예외)** 범위 연산자 주위에는 사용하지 않음
- 단항 연산자는 공백 사용 안함
- `if`, `when`, `for`, `while` 블록의 여는 괄호 사이에 공백 사용
- 주 생성자 선언, 메소드 선언, 메소드 호출에서 여는 괄호 앞에 공백 사용 안함

```Kotlin
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```

- `(`, `[`의 뒤와 `)`, `]`의 앞에 공백 사용 안함
- `.` 또는 `?.` 앞 뒤에 공백 사용 안함
- `//` 뒤에 공백 사용
- specify type parameters를 지정하는데 사용하는 `<>` 주위에는 공백 사용 안함
- `::` 주위에는 공백 사용 안함
- Nullable type을 표시하는데 사용하는 `?` 앞에는 공백 사용 안함

### 콜론(`:`)
아래의 경우 콜론 앞에 공백 사용
- 타입과 슈퍼 타입을 분리하는데 사용
- 슈퍼클래스 생성자 또는 같은 클래스의 다른 생성자에 위임할 때
- object 키워드 뒤에 사용

콜론이 선언과 type을 분리하는데 사용할 때는 콜론 앞에 공백 사용 안함

콜론 뒤에는 항상 공백 사용

```Kotlin
abstract class Foo<out T : Any> : IFoo {
    abstract fun foo(a: Int): T
}

class FooImpl : Foo() {
    constructor(x: String) : this(x) { /*...*/ }

    val x = object : IFoo { /*...*/ }
}
```

### 클래스 헤더
주 생성자의 매개변수가 적으면 한 줄에 작성 가능

```Kotlin
class Person(id: Int, name: String)
```

주 생성자의 매개변수가 많으면 각 매개변수가 들여쓰기된 별도의 줄에 있도록 서식 지정<br/>
닫는 괄호는 새 줄에 사용<br/>
상속을 사용하는 경우 슈퍼클래스 생성자 호출 또는 구현된 인터페이스 목록은 닫는 괄호와 같은 줄에 작성

```Kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { /*...*/ }
```

다중 인터페이스의 경우 슈퍼클래스 생성자 호출을 먼저 작성<br/>
각 인터페이스는 다른 행에 작성

```Kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { /*...*/ }
```

긴 상위 유형 목록이 있는 클래스의 경우 콜론 다음에 줄 바꿈을 넣고 모든 상위 유형 이름의 시작열을 맞춘다.

```Kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne {

    fun foo() { /*...*/ }
}
```

클래스 헤더가 길 때 클래스 헤더와 본문을 명확하게 구분하려면 클래스 헤더 다음에 빈 줄을 넣거나 여는 중괄호를 별도의 줄에 넣습니다.

```Kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne
{
    fun foo() { /*...*/ }
}
```

생성자 매개변수에는 공백 4

### Modifier
Modifier : 선언이나 변수 앞에 붙이는 예약어<br/>
여러 Modifier를 쓰는 경우 아래 순서로 입력

```
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation / fun // as a modifier in `fun interface`companion
inline
infix
operator
data
```

모든 annotation은 modifier 앞에 둔다.

```Kotlin
@Named("Foo")
private val foo: Foo
```

라이브러리에서 작업하지 않는한 중복 modifier는 생략

### Annotations
어노테이션은 일반적으로 어노테이션이 붙을 선언 이전에 같은 들여쓰기로 별도의 줄에 위치

```Kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class JsonExclude
```

인수가 없는 어노테이션은 여러개를 같은 줄에 작성 가능

```Kotlin
@JsonExclude @JvmField
var x: String
```

인수가 없는 단일 어노테이션은 선언과 같은 줄에 작성 가능

```Kotlin
@Test fun foo() { /*...*/ }
```

### Function
함수 시그너치가 한 줄에 들어가지 않으면 다음과 같이 작성

```Kotlin
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType,
): ReturnType {
    // body
}
```

함수 매개변수에는 공백 4개 사용

단일 표현식으로 구성된 바디를 가진 함수는 표현식 바디 사용 선호

```Kotlin
fun foo(): Int {     // bad
    return 1
}

fun foo() = 1        // good
```

### 속성 서식
간단한 읽기 전용 속성의 경우 한 줄 형식 사용

```Kotlin
val isEmpty: Boolean get() = size == 0
```

보다 복잡한 속성의 경우 항상 키워드 `get`과 `set`을 별도의 줄에 입력

```Kotlin
val foo: String
    get() { /*...*/ }
```

이니셜라이저가 있는 속성의 경우 이니셜라이저가 길면 `=` 다음에 줄 바꿈을 하고 4칸 들여쓰기 한다.

```Kotlin
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

### 제어문
`if`나 `when`문의 조건이 여러 줄일 경우 항상 문장의 본문 주위에 중괄호 사용<br/>
조건의 두 번째 줄부터 앞에 4칸의 공백 삽입<br/>
조건을 닫는 소괄호는 여는 중괄호와 함께 별도의 줄에 작성

```Kotlin
if (!component.isSyncing &&
    !hasAnyKotlinRuntimeInScope(module)
) {
    return createKotlinNotConfiguredPanel(module)
}
```

`else`, `catch`, `finally`, `do-while`문의 `while` 키워드의 같은 줄에 여는 중괄호 작성

```Kotlin
if (condition) {
    // body
} else {
    // else part
}

try {
    // body
} finally {
    // cleanup
}

```

`when`문에서 실행 부분이 한 라인 이상일 경우 인접한 실행 블록을 빈 줄로 분리

```Kotlin
private fun parsePropertyValue(propName: String, token: Token) {
    when (token) {
        is Token.ValueToken ->
            callback.visitValue(propName, token.value)

        Token.LBRACE -> { // ...
        }
    }
}
```

짧은 조건, 실행 라인은 중괄호 없이 한 라인에 작성

```Kotlin
when (foo) {
    true -> bar() // good
    false -> { baz() } // bad
}
```

### 메소드 호출
메소드 호출 시에 인자들이 길어 한 줄에 작성하지 못할 경우 여는 소괄호 뒤에서 줄바꿈<br/>
서로 연관있는 인자끼리 묶어서 작성<br/>

```Kotlin
drawSquare(
    x = 10, y = 10,
    width = 100, height = 100,
    fill = true
)
```

인자 이름과 값을 구분하는 `=` 앞, 뒤에 공백 삽입

### 함수 호출 체이닝 구조
옵셔널 체이닝을 사용하거나 체이닝을 사용하는데 한 줄을 넘어간다면 `?.`와 `.`가 제일 앞에 오고 들여쓰기를 해서 작성

```Kotlin
val anchor = owner
    ?.firstChild!!
    .siblings(forward = true)
    .dropWhile { it is PsiComment || it is PsiWhiteSpace }
```

### 람다
- 파라미터를 나타내는 화살표 주위에 공백 사용
- 표현식의 중괄호 주위에 공백 사용
- 호출에 사용된 람다가 한 개인 경우 가능한 소괄호 제거(마지막 인자가 람다이거나, 인자가 람다 뿐이거나)
- 람다의 파라미터가 하나뿐이고 그 타입을 컴파일러가 추론 가능한 경우 `it` 사용 가능

```Kotlin
list.filter { it > 10 }
```

람다에 `label`을 할당할 경우 `label`과 여는 중괄호 사이에 공백 사용 안함

```Kotlin
fun foo() {
    ints.forEach lit@{
        // ...
    }
}
```

다중 라인 람다에서 파라미터의 이름을 선언할 때, 첫 줄에 파라미터 이름과 화살표를 선언하고 개행

```Kotlin
appendCommaSeparated(properties) { prop ->
    val propertyValue = prop.get(obj)  // ...
}
```

파라미터 목록이 한 줄로 표현하기 적합하지 않은 경우 파라미터 목록과 화살표를 들여쓰기와 함께 개행

```Kotlin
foo {
   context: Context,
   environment: Env
   ->
   context.configureEnv(environment)
}
```

### Trailing 콤마(,)

## 4. Documentation Comments
- 문서 주석을 사용할 경우 `/**`로 시작
- 각 줄에 `*` 사용
- 닫을 때는 `*/`

```Kotlin
/**
 * This is a documentation comment
 * on multiple lines.
 */
```

짧은 주석은 한 줄에 올 수 있다.

```Kotlin
/** This is a short documentation comment. */
```

- 일반적으로 `@param`과 `@return` 태그는 사용하지 말 것
- 파라미터 및 반환 값에 대한 설명을 주석 내용에 직접 포함시키고 언급된 모든 파라미터에 링크 추가
- 주석 내용의 흐름에 맞지 않는 장황한 설명이 필요한 경우만 `@param` 및 `@return` 사용

```Kotlin
// Avoid doing this:

/**
 * Returns the absolute value of the given number.
 * @param number The number to return the absolute value for.
 * @return The absolute value.
 */
fun abs(number: Int) { /*...*/ }

// Do this instead:

/**
 * Returns the absolute value of the given [number].
 */
fun abs(number: Int) { /*...*/ }
```

## 5. Avoid redundant constructs
필요없는 요소들은 모두 배제한다.<br/>
명확성을 위해 코드에 불필요한 구문 요소를 남겨두지 않는다.

- 아무것도 반환하지 않는 함수의 `Unit` 반환형
- 세미콜론
- 문자열 템플릿에서의 안써도 되는 중괄호

```Kotlin
// Unit 반환형
fun foo() { // ": Unit" is omitted here

}

// 문자열 템플릿에서의 안써도 되는 중괄호
println("$name has ${children.size} children")
```

## 6. Idiomatic use of language features
언어의 기능들을 관용적으로 사용하기

### 불변성(Immutability)
