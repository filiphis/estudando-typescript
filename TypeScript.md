# Aprendendo TypeScript Detalhadamente

Com o TypeScript podemos declarar tipagem para nossas variáveis, parâmetros de funções, retorno de funções, entre outras funcionalidades...

## Tipagem

Existe dois tipos de tipagem, são elas:

- Tipagem dinâmica
- Tipagem estática

### Tipagem Dinâmica

- O tipo de uma variável é associando com o seu valor e não é explicitamente declarado.

### Tipagem Estática

- O tipo de uma variável e explicitamente declarado.
- Após ser informado um tipo, este não pode mais ser alterado.
- Os valores assinalados á uma variável precisam respeitar o tipo previamente definido.

## Tipos

### Tipos básicos

- number
- string
- boolean
- any

### Tupla

É uma forma de definir uma tipagem para a ordem de um array.

Por exemplo:

```tsx
let person: [string, number];
person = ["Luiz", 28];
```

#### Lista de Tuplas

Também é possível criar uma lista de tuplas.

Por exemplo:

```tsx
let persons: [string, number][];
persons = [
  ["Gustavo", 2],
  ["Luiz", 28],
];
```

### Intersections

É utilizado para definirmos quando um dado pode ser de um tipo, ou (|) de outro.

Por exemplo:

```tsx
const productId: string | number;
```

### Enum

É utilizado quando queremos criar um conjunto limitado de valores.

Por exemplo:

```tsx
enum Direction {
  Left = "esquerda",
  Right = "direita",
}

const direction = Direction.Left;
```

### Type Assertions

É utilizado quando queremos tratar uma variável de um tipo, como outro tipo.

Por exemplo:

```ts
const productName: any = "Bone";

let itemId = productName as string; // productName é informado como uma string, e itemId é uma string, e não any.
let itemId = <string>productName; // Faz a mesma coisa que o código acima /\.
```

## Funções no TypeScript

Com TypeScrip também é possível definir tipagem para os parâmetros e retorno de uma função.

Exemplo de utilização em funções:

```ts
function sum(a: number, b: number, c?: string): number {}
// Tipando parâmetros e retorno.
// Parâmetros podem ser opcionais.
```

#### Tipando funções com interfaces

Também podemos tipar os parâmetros e retorno de funções utilizando uma interface.

Segue exemplo:

```ts
interface MathFunc {
  (x: number, y: number): string;
  // função deve receber dois parâmetros numéricos e seu retorno é do tipo string.
}

const sum: MathFunc = (x: number, y: number): number => x + y;
// Irá ocorrer erro pois a interface informa que o retorno deve ser string,
// E ao criarmos a função informamos que o retorno será number.
```

OBS: A interface irá considerar tanto a tipagem dinâmica, quanto estática.

### Void

Quando uma função não possui nenhum retorno, o "retorno" dela será do tipo `void`.

## Objetos

Podemos tipar objetos inteiros utilizando o `type` ou a `interface`.
Ao criar esse tipo, ele pode ser utilizado em variáveis ou funções, e elas devem respeitar o tipo que foi criado, tanto no nome e quantidade de parâmetros, como no tipo de cada um desses parâmetros.

### Type

Exemplo de utilização do type:

```ts
// Criando um tipo de objeto:
type User = {
  firstName: string;
  lastName: string;
  email: string:
  password: string;
  age: number;
  country?: string; // interrogação informa que um valor é opcional.
};

const userName: User;
userName = {
///... valor ficam aqui, e respeitando o type, visto que essa variável é do tipo User.
}
```

### Interface

São bem parecidas com os types.

Algumas funcionalidades diferentes:

- É possível definir que uma propriedade será somente de leitura `readyonly`, ou seja, após o valor do objeto ser definido, não poderá mais ser alterado.

Por exemplo:

```ts
interface UserInterface {
  readonly email: string;
  password: string;
  minhaFunc(): string; // Define que esse tipo tem que ter essa função, e com esse tipo de retorno.
}

const userName: UserInterface = {
  email: "user@mail.com",
  password: "1234",
};

userName.email = "user_novo_email@mail.com";
// Irá ocorrer um erro, pois o campo email, após definido não pode ser alterado.
```

### Unions ( & )

Com unions é possível fazer com que um dado seja a união de dois **tipos** ou **interfaces**, ou seja, deverá ter a tipagem contida nos dois tipos informados.

Por exemplo:

```ts
type Person = {
  name: string;
  age: number;
  country: string;
};

type Author = {
  books: string[];
};

const authorName: Person & Author = {
  name: "Irineu",
  age: 99,
  country: "Brasil",
  books: ["nome do livro 1", "nome do livro 2"],
};
```

### Valores opcionais ( ? ) e non-null assertion ( ! )

Podemos definir em uma tipagem que determinando valor pode ser opcional, porem, isso pode gerar um problema.

Por exemplo, se informarmos que o country de um usuário é opcional e futuramente tentarmos utilizar o campo country, devemos ficar atentos, pois, como o campo é opcional, pode ser que ela seja undefined ou não.

Por exemplo:

```ts
type User = {
  name: string;
  age?: number; // age é opcional
};

const newUser: User = {
  name: "Luiz",
};

function checkAge(age: number) {
  return age >= 18;
}

checkAge(newUser.age);
// Irá ocorrer um erro no parâmetro, pois, age pode existir ou não.
```

Uma funcionalidade que podemos utilizar quando queremos **garantir** que um valor não será nulo é o **non-null assertion**.

Por exemplo:

```ts
checkAge(newUser.age!);
// Não irá ocorrer erro, pois o exclamação garante que a variável age irá existir.
```
