# React - Hook useState

O `useState` é um dos hooks mais importantes do React e permite que você adicione **estado** a componentes funcionais. Com ele, é possível criar variáveis que "guardam" valores que podem mudar ao longo do tempo e que, quando mudam, fazem o componente ser re-renderizado.

---

## O que é o useState?

- É uma função que retorna um **par**: o estado atual e uma função para atualizá-lo.
- Permite que componentes funcionais tenham **dados mutáveis**.

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
