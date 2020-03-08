# Coding Conventions

## Source code organization

### - Directory structure

- 루트 패키지가 생략된 패키지 구조를 권장  
- 코틀린에서는 여러 클래스를 한 파일에 넣을 수 있고, 파일의 이름도 마음대로 정할 수 있다.
- 만약 프로젝트 안의 모든 코드가 `org.example.kotlin` 패키지와 그 하위 패키지 안에 있다면, `org.example.kotlin` 패키지의 파일들은 루트 바로 아래에 있어야 하고, `org.example.kotlin.network.socket` 패키지의 파일들은 루트의 하위 폴더 `network/socket`에 있어야 한다.

### - Source file names

- 파일에 하나의 클래스만 있는 경우 파일의 이름은 클래스의 이름과 같아야 한다.  
- 파일에 여러 클래스가 있는 경우 파일의 내용을 설명하는 이름으로 지정한다.
    - Camel case 사용(`ProcessDeclarations.kt`)

### - Source file organization

- 여러 선언(클래스, 최상위 함수 등)들이 서로 밀접한 관련이 있고 코드가 몇 백 줄을 초과하지 않는 한, 같은 파일에 배치하는 것을 권장

### - Class layout

- 일반적으로 클래스의 내용들은 다음과 같이 정렬된다.
    - 프로퍼티 선언과 초기화 블록
    - 부 생성자
    - 메소드 선언
    - 동반 객체(Companion object)
- 중첩 클래스는 그 클래스를 사용하는 코드 다음에 놓는다.
- 중첩 클래스가 외부에서 사용되고, 클래스 내에서 참조되지 않는 경우 동반 객체 뒤에 마지막에 놓는다.

### - Interface implementation layout

- 인터페이스를 구현할 때, 인터페이스 구성 순서와 동일하게 유지해라.

## Naming rules

- 패키지의 이름은 항상 소문자이고 밑줄을 사용하지 않는다.
    - 만약 여러 문자를 사용하는 경우 Camel case 사용 가능
- 클래스와 객체 이름은 대문자로 시작하고 Camel case를 사용

```kotlin
open class DeclarationProcessor { /*...*/ }

object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
```

### - Function names

- 함수, 프로퍼티, 지역 변수의 이름은 소문자로 시작하고 Camel case를 사용

```kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

- 예외: 클래스의 인스턴스를 생성하기 위해 사용되는 팩토리 함수는 생성되는 클래스 이름과 같은 이름을 가질 수 있다.

```kotlin
abstract class Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun FooImpl(): Foo { return FooImpl() }
```

#### Names for test methods

- 테스트 코트에서 메소드 이름으로 ``(backticks)안에서 공백 사용 가능
- 테스트 코드에서 밑줄 사용 가능

```kotlin
class MyTestCase {
     @Test fun `ensure everything works`() { /*...*/ }
     
     @Test fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

### - Property names

- 상수 이름은 대문자와 밑줄을 사용

```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```

// 내용 추가해야함

## Formatting

- 들여쓰기는 4칸(탭 사용X)
- 중괄호는 이렇게

```kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```

- 세미콜론은 옵션

### - Horizontal whitespace

- 2항 연산 기호(빈칸O): `a + b`
- 범위 연산자(빈칸X): `0..i`
- 단항 연산자(빈칸X): `a++`
- 제어 흐름 키워드와 괄호(빈칸O): `if (...)`
- 주 생성자, 메소드 선언, 호출(빈칸X)

```kotlin
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```

- `(`, `[` 후 or `)`, `]` 전에는 빈칸X
- `.`앞뒤로 공백 X
    - `foo.bar().filter { it > 2 }.joinToString()`, `foo?.bar()`
- `class Map<K, V> { ... }`
- `Foo::class`, `String::length`
- `String?`

### - Class header formatting

- single line

```kotlin
class Person(id: Int, name: String)
```

- Classes with longer headers

```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { /* ... */ }
```

- For multiple interfaces

```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { /* ... */ }
```

- For classes with a long supertype list

```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne {

    fun foo() { /*...*/ }
}
```

- To clearly separate the class header and body when the class header is long

```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne 
{
    fun foo() { /*...*/ }
}
```

### - Modifiers

하나의 선언에서 여러 변경자를 가지고 있다면 다음과 같은 순서 적용

```kotlin
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
enum / annotation
companion
inline
infix
operator
data
```

### - Annotation formatting

인자가 없는 애노테이션은 한 줄에 배치 가능

```kotlin
@JsonExclude @JvmField
var x: String
```

### - File annotations

