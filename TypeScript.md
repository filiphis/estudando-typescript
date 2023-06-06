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
