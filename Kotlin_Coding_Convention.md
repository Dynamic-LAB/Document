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

