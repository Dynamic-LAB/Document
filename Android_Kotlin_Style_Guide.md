# Android_Kotlin_Style_Guide
Android Developers의 공식 스타일 가이드 문서를 따른다.<br/>
https://developer.android.com/kotlin/style-guide?hl=ko

# 1. 소스 파일
모든 소스 파일은 UTF-8로 인코딩되어야 한다.

## 이름 지정
소스 파일에 최상위 클래스가 하나 뿐인 경우 대소문자를 구분하는 클래스 이름과 `.kt` 확장자 반영

```Kotlin
// MyClass.kt
class MyClass { }
```

소스 파일에 최상위 수준 선언이 여러 개 있는 경우 파일의 콘텐츠를 설명하는 이름을 선택하고 PascalCase 적용

```Kotlin
// Bar.kt
class Bar { }
fun Runnable.toBar(): Bar = // …

// Map.kt
fun <T, O> Set<T>.map(func: (T) -> O): List<O> = // …
fun <T, O> List<T>.map(func: (T) -> O): List<O> = // …
```

## 특수문자

### 공백 문자
수평 공백 문자는 줄 마침 표시 시퀀스를 제외하고 소스 파일의 유일한 공백 문자

- 문자열과 문자 리터럴의 모든 다른 공백문자는 이스케이프 처리
- 들여쓰기에 탭 문자 사용 금지

### 이스케이프 시퀀스
특수 이스케이프 시퀀스 : `\b`, `\n`, `\r`, `\t`, `\'`, `\"`, `\\`, `\$`

## 구조
`.kt` 파일은 아래 순서로 구성

- 저작권 및 라이선스 헤더(선택)
- 파일 수준 주석
- Package
- Import
- 최상위 수준 선언

빈 줄을 하나만 사용해서 각 항목 분리

### 저작권/라이선스
파일에 저작권 또는 라이선스 헤더가 포함된 경우 맨 위에 여러 줄로 주석 삽입<br/>
KDoc 스타일 또는 한 줄 주석 사용 금지

```Kotlin
// good
/*
 * Copyright 2017 Google, Inc.
 *
 * ...
 */
 
// bad
/**
 * Copyright 2017 Google, Inc.
 *
 * ...
 */
 
// bad
// Copyright 2017 Google, Inc.
//
// ...
```

### 파일 수준 주석
use-site target '파일'을 포함하는 주석은 헤더 주석과 패키지 선언 사이에 배치

### Package
`package`문은 열 제한을 받지 않으며 줄바꿈하지 않는다.

### Import
클래스, 함수 및 속성의 `import`문은 단일 목록으로 그룹화, ASCII 정렬<br/>
모든 유형의 와일드카드 가져오기는 허용되지 않는다.<br/>
열 제한을 받지 않으며 줄바꿈하지 않는다.

### 최상위 수준 선언
`.kt` 파일은 최상위 수준에서 하나 이상의 유형, 함수, 속성, 또는 유형 별칭을 선언할 수 있다.

파일의 내용은 단일 테마에 중점<br/>
관련 없는 선언은 자체 파일로 분리, 단일 파일 내 공개 선언은 최소화되어야 한다.

파일 콘텐츠의 수와 순서에는 명시적인 제한이 적용되지 않는다.

소스 파일은 일반적으로 위에서 아래로 읽는다.<br/>
순서가 더 높은 선언을 이해하면 순서가 더 낮은 선언을 이해할 수 있도록 순서 지정<br/>

각 클랫에서 특정한 논리적 순서를 사용할 것

### 클래스 멤버 정렬
클래스 내 멤버의 순서는 최상위 수준 선언과 동일한 규칙을 따른다.

# 2. 서식
## 중괄호
`else if`, `else` 분기가 없고 한 줄에 들어가는 `when` 분기 및 `if`문 본문에는 중괄호가 필요하지 않음

```Kotlin
if (string.isEmpty()) return

when (value) {
    0 -> return
    // …
}
```

`if`, `for`, `when` 분기 및 `do`-`while`문의 경우 본문이 비어 있거나 단일 구문만 포함하는 경우에도 중괄호가 필요

```Kotlin
if (string.isEmpty())
    return  // WRONG!

if (string.isEmpty()) {
    return  // Okay
}
```

다음 항목 준수

- 여는 중괄호 앞에 줄바꿈이 없음
- 여는 중괄호 뒤에서 줄바꿈
- 닫는 중괄호 전에 줄바꿈
- 중괄호로 구문이 종료되거나 함수, 생성자 또는 named 클래스의 본문이 종료되는 경우에만 닫는 중괄호 뒤에 줄바꿈

```Kotlin
return Runnable {
    while (condition()) {
        foo()
    }
}

return object : MyClass() {
    override fun foo() {
        if (condition()) {
            try {
                something()
            } catch (e: ProblemException) {
                recover()
            }
        } else if (otherCondition()) {
            somethingElse()
        } else {
            lastThing()
        }
    }
}
```

빈 블록 또는 블록 형식 구문은 다음과 같이 작성

```Kotlin
try {
    doSomething()
} catch (e: Exception) {
}
```

표현식으로 사용되는 `if/else` 조건문에서는 전체 표현식이 한 줄에 들어가는 경우에만 중괄호 생략 가능

```Kotlin
val value = if (string.isEmpty()) 0 else 1  // Okay

val value = if (string.isEmpty())  // WRONG!
    0
else
    1
    
val value = if (string.isEmpty()) { // Okay
    0
} else {
    1
}
```

## 들여쓰기
새 블록 또는 블록 형식 구문이 열릴 때마다 들여쓰기가 4칸씩 증가<br/>
블록이 끝나면 이전 들여쓰기 수준으로 복귀

## 줄바꿈
한 줄에 한 구문만 작성할 것 = 각 구문 다음에 줄바꿈 삽입<br/>
세미콜론은 사용하지 않음<br/>

코드의 열 제한은 100자<br/>
이를 초과하는 경우 줄바꿈

**예외)**
- 열 제한을 준수할 수 없는 줄
- `package` 및 `import` 문
- 잘라서 셸에 붙여넣을 수 있는 주석의 명령줄

## 줄바꿈 위치
우선적으로 줄바꿈은 더 높은 구문 수준에서 하는 것이 좋음

- 연산자 또는 중위 함수 이름에서 행을 나누면 연산자 또는 중위 함수 이름 다음에 줄바꿈 발생
- `.`, `?.`, `::` 기호에서 행을 나누면 기호 앞에서 줄바꿈 발생
- 메소드 또는 생성자 이름은 뒤에 오는 열린 괄호에 연결된 상태로 유지
- 쉼표는 앞에 오는 토큰에 연결된 상태로 유지
- 람다 화살표는 앞에 오는 인수 목록에 연결된 상태로 유지

## 함수
함수 서명이 한 줄에 들어가지 않으면 각 매개변수 선언을 한 줄에 하나씩 표시한다.<br/>
이 형식으로 정의된 매개변수에서는 단일 들여쓰기 사용<br/>
닫는 괄호 및 반환 유형은 추가 들여쓰기 없이 한 줄에 하나씩 작성

```Kotlin
fun <T> Iterable<T>.joinToString(
    separator: CharSequence = ", ",
    prefix: CharSequence = "",
    postfix: CharSequence = ""
): String {
    // …
}
```

## 표현식 함수
함수에 표현식이 하나만 포함되는 경우 표현식 함수로 표현 가능

```Kotlin
override fun toString(): String {
    return "Hey"
}

override fun toString(): String = "Hey"
```

표현식 함수가 블록을 여는 경우에만 이 함수를 여러 줄로 줄바꿈

```Kotlin
fun main() = runBlocking {
  // …
}
```

그렇지 않은 경우 표현식 함수가 증가하여 줄바꿈이 필요한 경우 일반 함수 본문, `return` 선언 및 일반 표현식 줄바꿈 규칙을 대신 사용

## 속성
속성 이니셜라이저가 한 줄에 들어가지 않을 경우 등호 뒤에서 줄바꿈하고 들여쓰기 사용

```Kotlin
private val defaultCharset: Charset? =
        EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

`get` 또는 `set` 함수를 선언하는 속성은 일반 들여쓰기를 적용하여 한 줄에 하나씩 입력<br/>
함수와 동일한 규칙을 사용하여 형식 지정

```Kotlin
var directory: File? = null
    set(value) {
        // …
    }
```

읽기 전용 속성에서는 한 줄에 들어가는 더 짧은 구문을 사용할 수 있다.

```Kotlin
val defaultExtension: String get() = "kt"
```

## 공백
### 수직 공백
빈 줄이 하나 표시

- 클래스의 연속하는 멤버 사이(속성, 생성자, 함수, 중첩 클래스 등)
  - **예외)** : 두 개의 연속하는 속성 사이에 다른 코드가 없는 경우 두 속성 사이의 빈 줄은 선택사항
  - 속성의 논리적 그룹을 만들고 속성을 지원 속성과 연결하는데 필요한 경우에 사용
- 코드를 논리 하위 섹션으로 구성하는 데 필요하다면 식 사이에 빈 줄 삽입
- 함수의 첫 번째 문 앞, 클래스의 첫 번째 멤버 앞 또는 클래스의 마지막 멤버 뒤에 선택적으로 빈 줄을 넣습니다.

### 수평 공백
언어 또는 다른 스타일 규칙에 필요할 때와 리터럴, 주석 및 KDoc를 제외하면 단일 공백이 다음 위치에만 표시

- 예약어는 같은 줄에서 뒤에 오는 여는 중괄호와 구분
- 예약어는 같은 줄에서 앞에 오는 닫는 중괄호와 구분
- 여는 중괄호 앞
- 이항연산자의 앞, 뒤
- 람다 식의 화살표 앞, 뒤
- 멤버 참조의 두 콜론 `::`, 점 구분자 `.`, 범위 연산자 `..`는 예외
- 기본 클래스 또는 인터페이스를 지정하기 위해 클래스 선언에 사용된 경우나 일반 제약조건의 `where`절에 사용된 경우만 `:` 앞에 공백 삽입

```Kotlin
// WRONG!
class Foo: Runnable
// Okay
class Foo : Runnable

// WRONG
fun <T: Comparable> max(a: T, b: T)
// Okay
fun <T : Comparable> max(a: T, b: T)

// WRONG
fun <T> max(a: T, b: T) where T: Comparable<T>
// Okay
fun <T> max(a: T, b: T) where T : Comparable<T>
```

- 쉼표 또는 콜론 뒤
- 단일 줄 주석 `//` 앞, 뒤에 공백 허용

## 특정 구성
### Enum 클래스
함수와 상수에 대한 문서가 없는 열거형은 필요에 따라 한 줄로 서식 지정 가능

```Kotlin
enum class Answer { YES, NO, MAYBE }
```

열거형의 상수가 별도의 줄에 배치되는 경우 상수가 본문을 정의하는 경우를 제외하고 빈 줄이 필요하지 않음

```Kotlin
enum class Answer {
    YES,
    NO,

    MAYBE {
        override fun toString() = """¯\_(ツ)_/¯"""
    }
}
```

enum 클래스는 클래스이므로 모든 다른 클래스 서식 지정 규칙이 적용

### 주석
멤버 또는 유형 주석은 주석 처리된 구문 바로 앞에 별도의 줄로 입력

```Kotlin
@Retention(SOURCE)
@Target(FUNCTION, PROPERTY_SETTER, FIELD)
annotation class Global
```

인수가 없는 주석은 한 줄로 입력할 수 있다.

```Kotlin
@JvmField @Volatile
var disposable: Disposable? = null
```

인수가 없는 주석이 하나만 있는 경우 선언과 동일한 줄에 입력할 수 있다.

```Kotlin
@Volatile var disposable: Disposable? = null

@Test fun selectAll() {
    // …
}
```

`@[...]` 구문은 명시적 use-site target에만 사용할 수 있으며, 한 줄에 인수가 없는 두 개 이상의 주석을 결합하는 데만 사용할 수 있다.

```Kotlin
@field:[JvmStatic Volatile]
var disposable: Disposable? = null
```

### 암시적 반환/속성 유형
표현식 함수 본문 또는 속성 이니셜라이저가 스칼라 값이거나 반환 유형을 본문에서 명확하게 추론할 수 있는 경우 생략할 수 있다.

```Kotlin
override fun toString(): String = "Hey"
// becomes
override fun toString() = "Hey"

private val ICON: Icon = IconLoader.getIcon("/icons/kotlin.png")
// becomes
private val ICON = IconLoader.getIcon("/icons/kotlin.png")
```

라이브러리를 작성할 때 명시적 유형 선언은 공개 API의 일부인 경우에만 유지

## 이름 지정
- 식별자에는 ASCII 문자와 숫자만 사용
- 특정 경우에만 `_`로 표시
- 각 유효 식별자 이름은 정규표현식 `\w+`와 일치

`name_`, `mName`, `s_name`, `kName`과 같이 특수 접두사 또는 접미사는 지원 속성의 경우를 제외하고 사용하지 않는다.

### 패키지 이름
패키지 이름은 모두 소문자이며 연속 단어는 `_` 없이 연결

```Kotlin
// Okay
package com.example.deepspace
// WRONG!
package com.example.deepSpace
// WRONG!
package com.example.deep_space
```

### 유형 이름
클래스 이름은 PascalCase로 작성되며 일반적으로 명사 또는 명사구

인터페이스 이름은 명사 또는 명사구 이지만 형용사 또는 형용사구를 대신 사용하는 경우도 있다.

테스트 클래스의 이름은 테스트 중인 클래스의 이름으로 시작하고 `Test`로 끝난다.

### 함수 이름
함수 이름은 camelCase로 작성되며 일반적으로 동사 또는 동사구

이름의 논리적 구성요소를 구분하기 위해 테스트 함수 이름에 `_` 사용 가능

```Kotlin
@Test fun pop_emptyStack() {
    // …
}
```

`Unit`을 반환하는 `@composable`로 주석처리된 함수는 PascalCase이며 명사처럼 이름이 지정되어 있다.

```Kotlin
@Composable
fun NameTag(name: String) {
    // …
}
```

### 상수 이름
상수 이름에는 UPPER_SNAKE_CASE를 사용하며 `_`로 단어를 구분

상수는 맞춤 `get` 함수가 없는 `val` 속성이며 콘텐츠를 세부적으로 변경할 수 없고 함수에 감지할 수 있는 부작용이 없다.<br/>
여기에는 변경할 수 없는 유형과 이 유형의 변경할 수 없는 컬렉션, 스칼라, 문자열도 포함(`const`로 표시된 경우)<br/>
인스턴스의 관찰 가능한 상태가 변경될 수 있는 경우 인스턴스는 상수가 아니다. 객체를 변경하지 않으려는 것만으로는 충분하지 않음

```Kotlin
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")
val AGES = mapOf("Alice" to 35, "Bob" to 32)
val COMMA_JOINER = Joiner.on(',') // Joiner is immutable
val EMPTY_ARRAY = arrayOf()
```

상수의 이름은 일반적으로 명사 또는 명사구

상수 값은 `object` 내부 또는 최상위 선언으로만 정의 가능<br/>
상수의 요구사항을 충족하지만 `class`의 내부에 정의된 값은 상수가 아닌 이름 사용

스칼라 값인 상수는 `const` 변경자를 사용

### 상수가 아닌 이름
camelCase로 작성<br/>
인스턴스 속성, 로컬 속성, 매개변수 이름에 적용<br/>
일반적으로 명사 또는 명사구

```Kotlin
val variable = "var"
val nonConstScalar = "non-const"
val mutableCollection: MutableSet = HashSet()
val mutableElements = listOf(mutableInstance)
val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
val logger = Logger.getLogger(MyClass::class.java.name)
val nonEmptyArray = arrayOf("these", "can", "change")
```

### 지원 속성
지원 속성이 필요한 경우 밑줄 처리된 접두사를 제외하고 일므이 실제 속성의 이름과 정확히 일치해야 한다.

```Kotlin
private var _table: Map? = null

val table: Map
    get() {
        if (_table == null) {
            _table = HashMap()
        }
        return _table ?: throw AssertionError()
    }
```

### 유형 변수 이름
각 유형 변수의 이름은 다음 두 스타일 중 하나로 지정

1. 단일 대문자, 필요에 따라 단일 숫자가 뒤에옴 (Ex: `E`, `T`, `X`, `T2`)
2. 클래스에 사용된 형식으로 된 이름, 대문자 `T`가 뒤에옴 (Ex: `RequesT`, `FooBarT`)

### camelCase
영어 구를 카멜 표기법으로 변환할 수 있는 방법

구문 형식의 이름으로 시작:
1. 구문을 일반 ASCII로 변환하고 모든 `'`를 삭제
2. 공백 및 나머지 구두점(일반적으로 `-`)에서 분할하여 단어로 나눈다.
3. 모두 소문자(두문자어 포함)인 경우 다음 중 하나를 실행
  - 파스칼 표기법을 적용하려면 각 단어의 첫글자를 대문자로 시작
  - 카멜 표기법을 적용하려면 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 시작
4. 마지막으로 모든 단어를 단일 식별자로 결합

![image](https://user-images.githubusercontent.com/58630483/111024465-423d4c00-8422-11eb-8959-34f3b5d3f814.png)

## 도움말
### 형식 지정
KDoc 블록의 기본 형식

```Kotlin
/**
 * Multiple lines of KDoc text are written here,
 * wrapped normally…
 */
fun method(arg: String) {
    // …
}
```

단일 행의 예

```Kotlin
/** An especially short bit of KDoc. */
```

기본 형식은 항상 허용<br/>
주석 마커를 포함하여 전체 KDoc 블록이 한 줄에 들어가는 경우 단일 줄 형식이 대체될 수 있다.<br/>
이는 블록 태그가 없는 경우에만 적용

### 단락
빈 줄 하나, 즉 정렬된 선행 별표(`*`)만 포함하는 줄은 단락 사이와 블록 태그(있는 경우) 그룹 앞에 표시됩니다.

### 블록 태그
사용되는 표준 블록 태그는 `@constructor`, `@receiver`, `@param`, `@property`, `@return`, `@throws`, `@see` 순으로 표시<br/>
빈 설명으로 표시되지 않음<br/>
블록 태그가 한 줄에 들어가지 않는 경우 연속된 줄은 `@`위치에서 4칸 들여쓰기

### 요약 프래그먼트
각 KDoc 블록은 요약 프래그먼트로 시작<br/>
이 프래그먼트는 클래스, 메서드 색인과 같은 특정 컨텍스트에 표시되는 텍스트의 유일한 부분이므로 매우 중요

프래그먼트는 명사구 또는 동사구이며 전체 문장이 아님

`A 'foo' is a...` 또는 `This method returns...`로 시작하지 않고 완전한 명령문을 형성할 필요도 없다.

프래그먼트는 전체 문장인 것처럼 대문자 및 구두점 처리

### 사용
최소한 KDoc는 모든 `public` 유형과 그런 유형의 모든 `public` 또는 `protected` 멤버에 제공되며 아래와 같은 몇 가지 예외가 존재

1. 설명이 필요없는 함수
foo 반환을 제외하고 실제로 달리 언급할 가치가 없는 경우 KDoc는 단순하고 명확한 함수 및 속성에 선택사항

이 예외를 인용하여 일반적인 독자가 알아야하는 관련 정보 생략을 정당화하는 것은 적절하지 않다.<br/>
Ex) `getCanonicalName` 함수 또는 `canonicalName` 속성에서 일반 독자가 표준 용어의 의미를 모를 수도 있는 경우 `/** Returns the canonical name. */`이라는 근거를 알려주는 문서를 생략하면 안된다.

2. 재정의
KDoc가 상위 유형 메소드를 재정의하는 메소드에 항상 존재하는 것은 아니다.

# 3. Gradle

## Dependencies
- 라이브러리를 추가할때 외부 라이브러리의 라이센스 고지 추가
- 라이브러리의 버전은 `+`로 적지 말고 반드시 명시
