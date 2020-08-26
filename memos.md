# 型について

```typescript
const name = "hello";

let nameChange = "hello";
nameChange = "hello2";

let username: string = "Hello";
let dummyNum: number = 2;
let bool: boolean = true

let array1: boolean[] = [true, false, false];
let array2: (string | number)[] = [0, 1, "hello"]

interface NAME {
  first: string;
  last: string;
}

let nameObj: NAME = { first: "yacobi", last: "yen" };

interface NAME {
  first: string;
  last: string | null; // string or nullを受け取れる
}

let nameObj: NAME = { first: "yacobi", last: "yen" };

const func1 = (x: number, y:number): number => {    // ):numberで返り値の型を指定できる
    return x + y;
}
```

オブジェクト型はキーに事前に設定した以外の型を入れるとエラーが発生する
nullもnull型で定義される
関数の返り値も型指定できる

## Intersection Types
複数の型を結合する処理

```typescript
type PROFILE = {
    age: number;
    city: string;
};

type LOGIN = {
    username: string;
    password: string;
};

// PROFILEとLOGINを結合する処理
type USER = PROFILE & LOGIN;

const userA: USER = {
    age: 30,
    city: "Tokyo",
    username: "xxx",
    password: "yyy",
};
```

## Union Types
変数が受けとれる型を制限する処理

```typescript
// Union Types
let value: boolean | number
value = true
value = "hello" // ←エラーとなる
value = 10;

// 配列の場合
let arrayUni: (number | string)[];
arrayUni = [0, 1, 2, "Hello"];
```

## Literal Types
代入する値の制限ができる

```typescript
let company: "FaceBook" | "Google" | "Amazon";
company = "Amazon"
company = "Apple" // ←tエラーとなる

let memory: 256 | 512;
memory = 512;
memory = 1; // ←エラーとなる
```

## Typeof
宣言済みの変数を継承する処理が可能

```typescript
let msg: string = "Hi";
let msg2: typeof msg;
msg2 = "Hello";

let animal = {cat: "small cat"};
let newAnimal: typeof animal = {cat: "big cat"};
```

jsonオブジェクトを継承するときとかに有用

## keyof
```typescript
type KEYS = {
    primary: string;
    secondary: string;
};
let key: keyof KEYS;    // keyをUniontypeとして宣言される
```

## typeof + keyof

```typescript
const SPORTS = {
    soccer: "Soccer",
    baseball: "Baseball",
};

let keySports: keyof typeof SPORTS;     // typeofで型を継承しつつkeyをUniontypeで宣言する
```

## enum
列挙型
自動で連番を付ける型となっている

```typescript
enum OS {
    Windows,    // 1
    Mac,        // 2
    Linux,      // 3
}

interface PC {
    id: number;
    OSType: OS;
}

const PC1: PC = {
    id: 1,
    OSType: OS.Windows
};

const PC2: PC = {
    id: 2,
    OSType: OS.Mac
};
```

## 型の互換性
```typescript
const comp1 = "test";
let comp2: string = comp1;      // 抽象度の高い文字型により抽象度の低い文字型は代入できる

let comp3: string = "test";
let comp4: "test" = comp3;      // 抽象度の低い文字リテラル型に抽象度の高い文字型は代入できない

let funcComp1 = (x: number) => {};
let funcComp2 = (x: string) => {};

funcComp1 = funcComp2;          // 引数の型が違うためエラーとなる
```

## Generics
propsの型指定のときに使われる

```typescript
interface GEN<T> {      // Tはエイリアスで型が定まっていない状態テンプレートのみ作って変数の型は決めないで作るもの
    item: T;
}
const gen0: GEN<string> = {item: "hello"};

const gen0: GEN<number> = {item: 12};

interface GEN1<T=string> {      // エイリアスにデフォルトの型を指定できる
    item: T;
}

interface GEN2<T extends string | number> {      // エイリアスをstringとnumberのみ入れれるように制限できる
    item: T;
}

function funcGen<T>(props: T) {
    return {item: props}
}
const gen6 = funcGen<string>("test");
const gen6 = funcGen<string | null>("test");
const gen6 = funcGen("test");       // エイリアスに明示的に型が指定されていなくても型推論が通る

function funcGen1<T extends string | null>(props: T) { // エイリアスをstringとnullのみ入れれるように制限できる
    return {item: props}
}


interface Props {
    price: number;
}

function funcGen3<T extends Props>(props: T) {
    return {value: props.price}
}

const gen10 = funcGen3({price: 10});

// arrow関数で書く場合
const funcGen4 = <T extends Props>(props: T) => {
    return { value: props.price}
}
```

## json型推論
```typescript
import Data from "./data.json"

type USERS = typeof Data;   // jsonデータの構造(keyと型)を取得できる
```

# React Hooks

```typescript

const App: React.FC = () => {
    return {
        <div>
    }
}