# Basic Types

## TypeScript types vs JavaScript types

타입스크립트는 개발시에 타입이 정해지고, 자바스크립트는 런타임 시에 타입이 정해진다.
그래서 타입스크립트는 한 스텝 먼저 에러를 확인 가능하다.

타입스크립트에서는 자바스크립트에서 기대하는 것과 동일한 타입을 지원하며, 개발을 돕기 위해 추가적인 열거 타입을 제공한다.

### TypeScript에서 제공하는 데이터 타입
1. JavaScript 기본 자료형
  - Boolean
  - Number
  - String
  - Null
  - Undefined
  - Symbol
  - Array : object 형
2. 프로그래밍을 도울 몇가지 추가 타입 -> 타입 시스템의 안정성을 도와주는 역할.
  - Any, Void, Never, Unknown
  - Enum
  - Tuple : object 형


## Primitive Type
오브젝트와 레퍼런스 형태 (참조형)이 아닌 실제 값을 저장하는 자료형.
프리미티브 형의 내장 함수를 사용 가능한 것은 자바스크립트 처리 방식 덕분.
- boolean
- number
- string
- undefined
- null
- symbol


literal 값으로 Primitive 타입의 서브 타입을 나타낼 수 있다.
`3.14` 라는 숫자는 전체 Number 타입의 서브 타입.
`'hello'` 는 전체 String 타입의 서브 타입.
`true`는 전체 Boolean 타입의 서브 타입 두 개 (true, false) 중 하나

또는 래퍼 객체로 만들 수 있다.
```
new Boolean(false); // typeof new Boolean(false) : 'object'
new String('hello'); // typeof new String('hello') : 'object'
new Number(42); // typeof new Number(42) : 'object'
```

타입스크립트에서는 래퍼 객체를 타입으로 사용하면 안됨.
래퍼 객체 !== 프리미티브 타입


## boolean

```
let isDone: boolean = false;
isDone = true;
console.log(typeof isDone);

// Primitive 타입과 래퍼 객체 비교
let isOk: Boolean = true;
let isNotOk: boolean = new Boolean(true); // error
```

## number

```
let decimal: number = 6; // 10진수 리터럴
let hex: number = 0xf00d; // 16진수 리터럴
let binary: number = 0b1010; // 2진수 리터럴
let octal: number = 0o744; // 8진수 리터럴
let notAnumber: number = NaN;
let underscoreNum: number = 1_000_000; // 알아보기 쉽게 표기 가능
```
