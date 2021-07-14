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

## string
```
// 큰 따옴표 작음 따옴표 모두 가능
let myName: string = "Soyoung";

// Template String
let fullName: string = "Mark Lee";
let age: number = 31;

let sentence: string = `Hello, My name is ${fullName}.

I'll be ${age + 1} years old next year.`;

console.log(sentence);
```

## symbol

- new Symbol 로 사용할 수 없음
- Symbol 함수를 이용해서 symbol 타입을 만들어낼 수 있다.
- 함수로 사용할 땐 대문자 Symbol, 타입으로 사용할 땐 소문자 symbol
- 각각의 심볼은 완전히 독립적으로 다른것을 가리킨다.
- ES2015에서 추가된 타입이기 때문에 사용하려면 tsconfig.js 파일에 설정 추가해줘야 한다.
  ```
  "lib": [
    "ES2015",
    "DOM"
  ]
  ```
- 프리미티브 타입의 값을 담아서 사용한다.
- 고유하고 수정불가능한 값으로 만들어준다.
- 주로 접근을 제어하기 위해 많이 쓰인다.

```
console.log(Symbol("foo") === Symbol("foo")); // false

const sym = Symbol();
const obj = {
  [sym]: "value",
};
// obj['sym'] // 접근 불가
obj[sym]; // 접근 가능
```

## null & undefined

- void와 마찬가지로 그 자체로는 그다지 유용하지 않다.
- 타입도 소문자, 값도 소문자

```
// 이 변수들에 할당할 수 있는 것들이 거의 없음!

let u: undefined = undefined;
let n: null = null;
```

- 그러나 컴파일 설정을 하게 되면 다르다.
- undefined와 null은 모든 다른 타입의 서브 타입이 된다.
- number에 null 또는 undefined를 할당할 수 있다는 의미
- 컴파일 옵션에서 `--strictNullChecks`를 사용하면 서브 타입 안되고, 자기 자신한테만 할당 가능 (void 예외)
  - 이 경우 null, undefined를 할당할 수 있게 하려면 union type을 이용해야 한다.

```
// tsconfig.json

"strict": true // 아래 모든 옵션들을 아우르는 옵션. 이걸 켜두면 다른 타입에 null, undefined 할당 불가능.
// "noImplicitAny": true,
// "strictNullChecks": true,
// "strictFunctionTypes": true,
// "strictBindCallApply": true,
// "strictPropertyInitialization": true,
// "noImplicitThis": true,
// "alwaysStrict": true,
```

```
// let myName: string = null; // error

// let u: undefined = null; // error
let v: void = undefined; // null은 불가능

// union 타입 (합집합)
let union: string | null = null;
union = 'Mark';
```

- 타입 가드 : 타입이 null일때만 어떻게 해라~ 조건 지정 가능.

### null
- 무언가가 있는데, 사용할 준비가 덜 된 상태.
- javaScript 런타임에서 null을 **typeof** 연산자로 찍어보면 object가 나온다.
- 타입스크립트에서는 null 타입은 null 값만 가질 수 있다.

### undefined
- 값을 할당하지 않거나, object의 property가 없을 때. 아예 준비가 안된 상태.
- javaScript 런타임에서 undefined를 **typeof** 연산자로 찍어보면 undefined가 나온다.


## object

- **primitive type이 아닌 것** 을 나타내고 싶을 때 사용하는 타입
- non-primitive type: not number, string, boolean, bigint(ES2020), symbol, null, undefined.

```
const person1 = { name: "Soyoung", age: 31 };
// person1: { name: string; age: number; }

const person2 = Object.create({ name: "Soyoung", age: 31 });
// ObjectConstructor.create(o: object | null)


// object literal
let obj1: object = {};
obj1 = {name: 'Soyoung'};
obj1 = [{name: 'Soyoung'}];
obj1 = 31; //  error
obj1 = 'Soyoung'; // error
obj1 = true; // error
obj1 = Symbol; // error

// create 함수 선언
declare function create(o: object | null): void;

create({ prop: 0 });
create(null);
create(33); // error
create('string'); // error
create(undefined); // error

// Object.create
Object.create(0); // error
```

## Array

- Array는 객체
- 사용방법 2가지 : Array<타입> or 타입[]
```
// 주로 이 방식을 더 많이씀.
let list: number[] = [1, 2, 3];

// 아래 방식은 jsx나 tsx에서 충돌날 수 있어서 사용 자제한다고 함.
// let list: Array<number> = [1, 2, 3];
```

- 요소들을 공통의 타입으로 묶을 수 있어야 Array.
- 그러나 다른 타입이 들어가더라도 union type으로 지정하면 된다.
```
let list: (number | string)[] = [1, 2, 3, "4"];
```

## Tuple

- 길이가 정해져 있고, 앞 뒤의 타입이 정해져 있는 형태에 쓰인다.
```
let x: [string, number];

x = ['hello', 10];
// x = [10, 'Soyoung']; // error

// x[2] = 'world'; // error
```

<img width="441" alt="스크린샷 2021-07-14 오후 1 01 19" src="https://user-images.githubusercontent.com/26291081/125559124-6d6c20ad-9fd1-4f5b-904d-c3106d96dfb7.png">


## any

- 어떠한 타입도 가능하다는 뜻의 타입
- 최대한 쓰지 않는 것이 타입 시스템의 안전성을 높인다.
- 그러나 사용할 수 밖에 없는 경우들이 있다. (단순히 로그를 찍어주거나, api 호출시 받는 값들...)

```
function returnAny(message: any): any {
  console.log(message);
}

const any1 = returnAny("리턴 아무거나");
// any1 type is any

any1.toString(); // type 에러 뜨지 않는다.
```
- `noImplicitAny` 옵션을 켜두면 any를 써야하는데 쓰지 않은 경우 오류 표시 뜬다.


- any는 객체를 통해서 전파된다.
- 모든 편의는 타입 안전성을 잃는 대가로 온다는 것을 기억해야 한다.
- 필요하지 않은 경우에는 any를 사용하지 않아야 한다.

```
let looselyTyped: any = {};

const d = looselyTyped.a.b.c.d; // 에러 나지 않고, d의 타입도 any가 된다.
```

아래 코드에서는 매개변수 타입이 any로 지정되면서 변수 a, b, c 모두 any로 흘러가게 되는 모습이다.
이럴 경우 any 타입이 전파되는 것을 막기 위해 가드를 세워줘야 한다.
```
function leakingAny(obj: any) {
  const a = obj.num;
  const b = a + 1;
  return b;
}

const c = leakingAny({ num: 0 });
```

아래 코드처럼 수정하면 변수 a, b, c 모두 number 타입임을 확신할 수 있게 되어 안전성을 갖는다.
```
function leakingAny(obj: any) {
  // a의 타입을 number로 지정해서 누수를 막는다.
  const a: number = obj.num;
  const b = a + 1;
  return b;
}

const c = leakingAny({ num: 0 });
```

## unknown

- any 타입의 위험성을 제한하기 위한 타입.
- any 처럼 어떠한 타입도 할당 가능하지만, unknown 타입을 사용하려고 할 때
  - 컴파일러가 타입을 추론할 수 있도록 타입 유형을 좁히거나(조건문 등으로 타입가드 적용)
  - type assertion 등으로 타입을 확정지어야만 사용 가능하다.
- 런타임 에러를 줄일 수 있을 것 같다.

```
declare const maybe: unknown;

// 그냥 할당하면 에러
const aNumber: number = maybe;

if (maybe === true) {
  // 이 안에서 maybe는 true type으로 지정된다. (타입 가드)
  
  const aBoolean: boolean = maybe;
  // const aString: string = maybe; // error
}

if (typeof maybe === 'string') {
  // 이 안에서 maybe는 string type으로 지정된다. (typeof 타입가드)
  
  const aString: string = maybe;
  // const aBoolean: boolean = maybe; // error
}
```

## never

- 일반적으로 return에 사용된다.
- return에 사용될 때, 함수의 body가 끝나지 않아야 한다. (throw Error 또는 무한 루프 등)

```
// 에러 던지기
function error(message: string): never {
  throw new Error(message);
}

function fail() {
  return error("failed");
}

// 무한 루프
function infiniteLoop(): never {
  while (true) {}
}
```

- never는 모든 타입의 subtype이며, 모든 타입에 할당 가능하다.
- 그러나 never에는 어떠한 타입도 할당할 수 없다. any 조차도...
- 잘못된 타입을 넣는 실수를 막고자 할 때 사용된다.

```
let a: string = 'hello';

if (typeof a !== 'string') {
  // a type is never
  // 어떠한 것도 할당할 수 없다.
  a;
}
```

```
declare const a: string | number;

if (typeof a !== 'string') {
  // a type is number
  a;
}
```

```
// 타입이 변수처럼 쓰이는 제네릭
// T가 만약에 string이면 'T & { [index: string]: any }' 이걸 만들고 아니면 never
type Indexable<T> = T extends string ? T & { [index: string]: any } : never;

// b type is never
const b: Indexable<{}> = ''; // error
```

## void

- 어떠한 타입도 가지지 않는 빈 상태
- 값은 없고 타입만 있어서 void라는 값을 쓸 순 없음.
- 변수에 void 타입을 annotation 하는 것이 아니라 값을 반환하지 않는 함수의 return 타입으로 주로 사용됨.
- 그 외에는 거의 사용성이 없음.

```
// 반환하는게 없어서 return type은 자동으로 void로 추론된다.
function returnVoid(message: string) {
  console.log(message);
  return;
  // return undefined; // 유일하게 허용되는 타입
}

// r type is void
// 그러나 void를 가지고 뭘 할 수 없기 때문에 변수에 할당하는 것도 의미없다.
const r = returnVoid('리턴이 없다.');
```
