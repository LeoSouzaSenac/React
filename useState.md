# React - Hook useState

O `useState` é um dos hooks mais importantes do React e permite que você adicione **estado** a componentes funcionais. Com ele, é possível criar variáveis que "guardam" valores que podem mudar ao longo do tempo e que, quando mudam, fazem o componente ser re-renderizado.

---

## O que é o useState?

- É uma função que retorna um **par**: o estado atual e uma função para atualizá-lo.
- Permite que componentes funcionais tenham **dados mutáveis**.

A função useState retorna um array com dois elementos. 
1-O valor atual do estado → neste caso, contador.
2-Uma função para atualizar esse valor → neste caso, setContador.

Claro! Vamos explicar **de forma didática** o que é **desestruturação de array (array destructuring)**, com exemplos simples e acessíveis — especialmente útil para iniciantes:

---

## 🎯 O que é "desestruturação de array"?

Desestruturação é uma **forma rápida de extrair valores de um array** (ou de um objeto) e armazená-los em variáveis.

### 📦 Imagine assim:

Você tem uma **caixa (array)** com dois itens:

```js
const caixa = [10, 20];
```

Normalmente, você acessaria assim:

```js
const a = caixa[0]; // 10
const b = caixa[1]; // 20
```

Com **desestruturação**, você escreve isso de forma mais elegante:

```js
const [a, b] = caixa;
```

Agora:

* `a` vale `10`
* `b` vale `20`

---

## 🧠 Por que usamos isso no `useState`?

Quando usamos `useState`, ele **retorna um array com dois itens**:

```js
[valorAtual, funcaoParaAtualizar]
```

Então fazemos a **desestruturação diretamente**:

```js
const [contador, setContador] = useState(0);
```

Isso é o mesmo que:

```js
const resultado = useState(0);
const contador = resultado[0];
const setContador = resultado[1];
```

Mas com desestruturação, fica **mais simples e legível**.

---

## 📌 Analogia com caixa de ovo:

Pense que o `useState` te entrega uma caixinha com **dois ovos**:

* O primeiro é o valor (ex: `0`)
* O segundo é uma função para mudar esse valor

Você pode "tirar os ovos da caixa" com desestruturação:

```js
const [valor, mudarValor] = useState(0);
```

---

## ✅ Resumo:

| Termo técnico    | Explicação simples                           |
| ---------------- | -------------------------------------------- |
| Array            | Lista de valores                             |
| Desestruturação  | Tirar os itens da lista e dar nomes          |
| `useState(0)`    | Retorna uma lista: \[valor, função]          |
| `[a, b] = array` | Extrai os dois valores e guarda em `a` e `b` |

---

## Sintaxe básica

```jsx
const [valorDoEstado, setValorDoEstado] = useState(valorInicial);
````

* `valorDoEstado`: a variável que guarda o estado atual.
* `setValorDoEstado`: função usada para atualizar o estado.
* `valorInicial`: o valor inicial que o estado vai ter.

---

## Exemplo simples

```jsx
import React, { useState } from 'react';

function Contador() {
  // Declarando o estado 'contador' com valor inicial 0
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Você clicou {contador} vezes</p>
      <button onClick={() => setContador(contador + 1)}>
        Clique aqui
      </button>
    </div>
  );
}

export default Contador;
```

### Como funciona:

* `contador` começa com o valor `0`.
* Quando o botão é clicado, chamamos `setContador(contador + 1)`.
* Isso atualiza o estado para o valor novo (`contador + 1`).
* O React re-renderiza o componente mostrando o valor atualizado.

---

## Dicas importantes

* A função de atualização (`setValorDoEstado`) **substitui** o valor antigo pelo novo.
* Se o novo estado depende do estado anterior, use uma função dentro do `set` para garantir o valor correto:

```jsx
setContador(prevContador => prevContador + 1);
```

* O estado pode ser de qualquer tipo: número, string, array, objeto, etc.

---

## Conclusão

O `useState` é fundamental para criar componentes interativos no React. Sempre que precisar de dados que mudam (como formulários, contadores, toggle, listas dinâmicas), use o `useState` para gerenciar esses valores.
