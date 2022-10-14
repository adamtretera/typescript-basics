---
theme: geist
highlighter: shiki
title: Typescript základy
---

# Typescript ? 

- **Javascript** se syntaxí pro typy
- větší kontrola nad kodem
- lepší debugování - a docs přímo v IDE
- Valid JS code je valid ts = mužeme se učit inkrementálně

---


# Start 

```shell
npm i -g typescript // instaluje typescript globálně

tsc --version // verze ts
```

- Pro zájemce 🙋 [compiler options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)


```shell
touch tsconfig.json // vytvoření configuračního jsonu
```
- Automaticky se přiřadí po spuštění
- Defaultní nastavení
```json
{
  "compilerOptions": {
    "target": "esnext"
  }
}
```
- Start
```shell
tsc index.ts
```
---


# Definování typů

## Implicitně 
- automaticky inferuje typy podle přiřazené hodnoty
```ts
let cislo = 13

cislo = "Ahoj" // Type error
```


## Explicitně 
- přímo určujeme typ
```ts
let cislo: number
cislo = "Ahoj" // Type error
```


---


# Nebo stackblitz
- typescript projekt

# Nebo typescript playground
- dobré pro zkoušení nových věcí v typescriptu a debug
- [https://www.typescriptlang.org/play](Playground)
---

## Typy 
- Primitivy `string`,`number`, a `boolean`
```ts
let cislo: number
let jeHotovo: boolean
let jmeno: string
```

## Array

- dva zápisy
```ts
let cisla: number[];

let texty: Array<string>;
```

---

## Tuples

- pro definování délky pole
```ts
let dveCisla: [string, number] = ["ahoj",0];

dveCisla[1] = 2;
```

## Any

- nespecifikujme typ - mužeme dělat co chceme - když nechcete psát typ

```ts
let obj: any = { x: 0 };


obj.foo();
obj.bar = 100;

```

- nehodí TS error, ale spadne až na chodu javascriptu při volání neexistující funkce `obj.foo()`
---

# Funkce
- parametr a return type
```ts
// Parametr type

function reverse(s: string) {
    return s.split("").reverse().join("");
}

reverse("hello world");

// Return type
function getFavoriteNumber(): number {
    return 26;
}
```

---

# Union types


```ts
let vysledek: number | string;
vysledek = [1] // type error

let jmeno: "Petr" | "Lukáš" | "Pavel" = "Pavel"
jmeno = "Test"
```

---

# Object types

```ts

const user = {
    name : "Petr",
    age : 13
}

function printUser(user: { name: string; age: number }) {
  console.log("The position's x value is " + user.name);
  console.log("The position's y value is " + user.age);
}
```
---

# Cvičení

```json
[
  {
    "userId": "1231231",
    "jobTitleName": "Developer", // Developer Designer Tester
    "firstName": "Ran",
    "lastName": "Vijay",
    "preferredFullName": "Ran Vijay",
    "employeeCode": "H9",
    "region": "DL",
    "phoneNumber": 33,
    "emailAddress": "ranvijay.k.ran@gmail.com"
  },
  ...
]

```

---


# Interfaces
- jak vytvořit typ pro objekt, který chci použít někde jinde

```ts
interface User {
  name: string;
  age: number;
}

interface  Article {
  title: string;
  content: string;
}

```

---


# Type Aliases
- pro vytvoření názvu (aliasu) nějakému typu
- umožňuje nám využívat typy znova

```ts
type User = {
  name: string;
  age: number;
};


function printUserInfo(user: User) {
  console.log("User: " + user.name + ": " + user.age)
}

```

- většinou používáme pro vytvoření **Union typů**

  ```ts
  type Username = "Petr" | "Lukáš" | "Tomáš"; // Literal string
  type Age = 17 | 18 | 19
  ```



---

# null nebo undefined

- Hodnota `undefined` znamená, že hodnota není přiřazena a neznáte její hodnotu
- Je to neúmyslná absence hodnoty
- Znamená to, že proměnná byla deklarována, ale ještě jí nebyla přiřazena hodnota
  
- Hodnota `null` znamená, že víte, že pole nemá hodnotu. Je to záměrná absence hodnoty.
- Přímo definováné developer




```ts
interface User { 
  name: string | null; // string nebo null
  age?: string // string nebo undefined
}

let foo:string;              
console.log(foo);         //undefined
 
```


---



# Type Assertions
- občas musíte říct typescriptu nějký typ, protože nemá způsob jak ho vědět
- např. dostanete něco z nějkého knihovny a vy víte jaký je to typ, ale knhiovna není na typována

```ts
zpracujData(data as MujTyp) // zavolám funkci zpracuj data a nemužu vědět typ
```
- je považován za bad practice
- téměř vždy se tomu dá nějkým způsobem vyhnout

---



# Praxe
```ts
interface User {
    id: string;
    name: string;
    email: string;
    isAdmin?: boolean;
    role: AccessRole
}

type AccessRole = "editor" | "viewer" 

type UserList = User[]

```


---

# Cvičení udělejte to stejné ale s Animals

```ts
{
  "jmeno": "Petr",
  "druh": "lev",
  "obrazek": "https://s25.postimg.org/55ot26lq7/lion_large.jpg",
  "potomci": [
    {
      "jmeno": "Pavel",
      "druh": "lev"
    },
    {
      "jmeno": "Novák",
      "druh": "lev"
    }
  ],
  "parents": [1232113, 1312313213],
  "jeOhrozeny": true
}
```
# Extendování

```ts
interface Animal {
  name: string
}

interface Klokan extends Animal {
  pocket: boolean;
}


type Animal = {
  name: string
}

type Bear = Animal & { 
  honey: boolean 
}
```
