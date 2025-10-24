# ⚛️ React Hook `useRef`

O **`useRef`** é um dos hooks mais versáteis e úteis do React.  
Ele serve para **armazenar valores mutáveis** (que não causam re-renderização) e **acessar elementos do DOM diretamente**.

---

## 🧠 O que significa “ref”?

A palavra **"ref"** vem de **“reference”** (referência).  
Em React, uma **ref** é como um **ponteiro para algo**, que permite guardar ou acessar um valor entre renderizações.

---

## 🚀 Importando o `useRef`

Para usar, basta importar do React:

```tsx
import { useRef } from "react";
````

---

## 🎯 Quando usar o `useRef`

| Situação                                   | O que o `useRef` faz                                          |
| ------------------------------------------ | ------------------------------------------------------------- |
| 🔍 Acessar um elemento HTML                | Permite controlar inputs, botões ou vídeos diretamente        |
| 💾 Guardar valores entre renders           | Armazena dados que não precisam re-renderizar o componente    |
| ⏱️ Controlar timers (intervals e timeouts) | Guarda a referência de um `setInterval` ou `setTimeout`       |
| ⚡ Evitar re-renderizações desnecessárias   | Mantém dados entre renders sem afetar o fluxo de renderização |

---

## 🧩 Estrutura básica

```tsx
const referencia = useRef(valorInicial);
```

* O `useRef()` cria um **objeto** com a propriedade `.current`
* O valor de `.current` **pode ser lido e alterado**
* Alterar `.current` **não causa re-renderização**

---

## 📘 Exemplo 1: Focar um input automaticamente

```tsx
import React, { useRef, useEffect } from "react";

export default function Exemplo1() {
  const inputRef = useRef<HTMLInputElement | null>(null); // cria a referência

  useEffect(() => {
    // Quando o componente montar, damos foco no input
    if (inputRef.current) {
      inputRef.current.focus();
    }
  }, []);

  return (
    <div style={{ padding: 20 }}>
      <h2>Exemplo 1 – Foco automático</h2>
      <input ref={inputRef} type="text" placeholder="Eu recebo foco!" />
    </div>
  );
}
```

🧠 Aqui:

* `ref={inputRef}` **liga** a ref ao input.
* `inputRef.current` **é o elemento HTML real**.
* Com `inputRef.current.focus()`, damos foco diretamente no campo.

---

## 🧮 Exemplo 2: Guardando valores entre renderizações

```tsx
import React, { useRef, useState } from "react";

export default function Exemplo2() {
  const [contador, setContador] = useState<number>(0);
  const renderCount = useRef<number>(0); // contador invisível

  renderCount.current += 1; // incrementa a cada renderização

  return (
    <div style={{ padding: 20 }}>
      <h2>Exemplo 2 – Guardando valores</h2>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
      <p>O componente foi renderizado {renderCount.current} vezes.</p>
    </div>
  );
}
```

🧠 Aqui:

* `renderCount` guarda o número de renders.
* Mesmo alterando `renderCount.current`, o componente **não re-renderiza**.
* É ideal para armazenar **dados que não influenciam a UI**.

---

## ⏱️ Exemplo 3: Controlando um intervalo (timer)

```tsx
import React, { useRef, useState, useEffect } from "react";

export default function Exemplo3() {
  const [tempo, setTempo] = useState<number>(0);
  const intervaloRef = useRef<number | null>(null);

  const iniciar = () => {
    if (!intervaloRef.current) {
      intervaloRef.current = window.setInterval(() => {
        setTempo((t) => t + 1);
      }, 1000);
    }
  };

  const parar = () => {
    if (intervaloRef.current) {
      clearInterval(intervaloRef.current);
      intervaloRef.current = null;
    }
  };

  useEffect(() => {
    return parar; // limpa o intervalo ao desmontar
  }, []);

  return (
    <div style={{ padding: 20 }}>
      <h2>Exemplo 3 – Timer com useRef</h2>
      <p>Tempo: {tempo}s</p>
      <button onClick={iniciar}>Iniciar</button>
      <button onClick={parar}>Parar</button>
    </div>
  );
}
```

🧠 Aqui:

* O `useRef` guarda o **ID do intervalo**.
* Isso permite parar o timer mesmo sem recriar funções.
* Evita erros de múltiplos `setInterval`.

---

## 💾 Exemplo 4: Salvando o valor anterior

```tsx
import React, { useState, useEffect, useRef } from "react";

export default function Exemplo4() {
  const [valor, setValor] = useState<string>("");
  const valorAnterior = useRef<string>("");

  useEffect(() => {
    valorAnterior.current = valor; // atualiza a cada render
  }, [valor]);

  return (
    <div style={{ padding: 20 }}>
      <h2>Exemplo 4 – Valor anterior</h2>
      <input
        type="text"
        value={valor}
        onChange={(e) => setValor(e.target.value)}
        placeholder="Digite algo"
      />
      <p>Valor atual: {valor}</p>
      <p>Valor anterior: {valorAnterior.current}</p>
    </div>
  );
}
```

🧠 Aqui:

* A cada mudança, o valor anterior é guardado em `.current`.
* Você pode comparar valores **entre renders** sem perder o histórico.

---

## 🎮 Exemplo 5: Controlando um vídeo com `useRef`

```tsx
import React, { useRef } from "react";

export default function Exemplo5() {
  const videoRef = useRef<HTMLVideoElement | null>(null);

  const pausarOuReproduzir = () => {
    if (videoRef.current) {
      if (videoRef.current.paused) {
        videoRef.current.play();
      } else {
        videoRef.current.pause();
      }
    }
  };

  return (
    <div style={{ padding: 20 }}>
      <h2>Exemplo 5 – Controlando um vídeo</h2>
      <video
        ref={videoRef}
        width="320"
        height="180"
        src="https://www.w3schools.com/html/mov_bbb.mp4"
      />
      <br />
      <button onClick={pausarOuReproduzir}>Play / Pause</button>
    </div>
  );
}
```

🧠 Aqui:

* `videoRef.current` acessa o elemento `<video>`.
* Podemos controlar **métodos nativos** como `play()` e `pause()`.

---

## ⚠️ Resumo rápido

| O que faz                  | Exemplo                                              |
| -------------------------- | ---------------------------------------------------- |
| Guardar valores mutáveis   | `const contador = useRef(0)`                         |
| Acessar elementos          | `<input ref={inputRef} />`                           |
| Não causa re-renderização  | `contador.current++`                                 |
| Guarda dados entre renders | `useEffect(() => valorRef.current = valor, [valor])` |

---

## 🧩 Dica de ouro

👉 Se você precisa **mostrar o valor na tela**, use `useState`.
👉 Se você precisa **guardar o valor sem atualizar a tela**, use `useRef`.

---

## 🧠 Conclusão

O **`useRef`** é perfeito para:

* Armazenar informações que não precisam re-renderizar o componente;
* Manipular elementos DOM diretamente;
* Controlar timers, valores anteriores e objetos persistentes.

Ele é o **gancho ideal** quando você precisa de **persistência de valor sem renderização.**

---

## 🧭 Próximos passos sugeridos

Depois de dominar o `useRef`, você pode estudar:

* **`useMemo`** → para memorizar valores calculados
* **`useCallback`** → para memorizar funções
* **`useReducer`** → para controlar estados complexos
