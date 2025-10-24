# ⚛️ React – Hook `useContext`

## 🧩 O que é **Contexto**?

No React, **contexto** é uma forma de **compartilhar dados entre componentes** sem precisar passar manualmente via props de um componente pai para seus filhos, netos, bisnetos, etc.

Ele serve para:

* Evitar **prop drilling** (passar props por muitos níveis)
* Criar **estados globais** acessíveis por vários componentes
* Centralizar dados que **não dependem de um componente específico**, como:

  * Tema claro/escuro
  * Usuário logado
  * Preferências do app
  * Configurações de idioma

O contexto funciona com **Provider** (quem fornece o dado) e **Consumer/Hook** (quem consome o dado).

---

## 📂 Estrutura de arquivos (React + TSX)

Para organizar corretamente, cada parte fica em seu arquivo:

```
/src
  /context
    TemaContext.tsx
    UsuarioContext.tsx
  /components
    ComponenteBotao.tsx
    Tela.tsx
    TelaUsuario.tsx
  App.tsx
```

---

## 🎬 Exemplo 1 – Tema claro/escuro

### 1️⃣ `TemaContext.tsx`

```tsx
import React, { createContext, useState, useContext, ReactNode } from "react";

// Tipo do contexto
type TemaContextType = {
  temaEscuro: boolean;
  setTemaEscuro: React.Dispatch<React.SetStateAction<boolean>>;
};

// Criando o contexto
const TemaContext = createContext<TemaContextType | undefined>(undefined);

// Provider
export const TemaProvider = ({ children }: { children: ReactNode }) => {
  const [temaEscuro, setTemaEscuro] = useState(false);

  return (
    <TemaContext.Provider value={{ temaEscuro, setTemaEscuro }}>
      {children}
    </TemaContext.Provider>
  );
};

// Hook personalizado para consumir
export const useTema = () => {
  const context = useContext(TemaContext);
  if (!context) throw new Error("useTema deve ser usado dentro de TemaProvider");
  return context;
};
```

---

### 2️⃣ `ComponenteBotao.tsx`

```tsx
import React from "react";
import { useTema } from "../context/TemaContext";

export const ComponenteBotao = () => {
  const { temaEscuro, setTemaEscuro } = useTema();

  return (
    <button onClick={() => setTemaEscuro(!temaEscuro)}>
      {temaEscuro ? "Mudar para claro" : "Mudar para escuro"}
    </button>
  );
};
```

---

### 3️⃣ `Tela.tsx`

```tsx
import React from "react";
import { useTema } from "../context/TemaContext";
import { ComponenteBotao } from "./ComponenteBotao";

export const Tela = () => {
  const { temaEscuro } = useTema();

  const estilo = {
    backgroundColor: temaEscuro ? "#333" : "#fff",
    color: temaEscuro ? "#fff" : "#000",
    height: "100vh",
    display: "flex",
    flexDirection: "column" as const,
    justifyContent: "center",
    alignItems: "center",
    gap: "20px",
  };

  return (
    <div style={estilo}>
      <h1>Tema atual: {temaEscuro ? "Escuro" : "Claro"}</h1>
      <ComponenteBotao />
    </div>
  );
};
```

---

### 4️⃣ `App.tsx`

```tsx
import React from "react";
import { TemaProvider } from "./context/TemaContext";
import { Tela } from "./components/Tela";

export default function App() {
  return (
    <TemaProvider>
      <Tela />
    </TemaProvider>
  );
}
```

---

## 🎬 Exemplo 2 – Usuário logado

### 1️⃣ `UsuarioContext.tsx`

```tsx
import React, { createContext, useState, useContext, ReactNode } from "react";

type Usuario = { nome: string } | null;
type UsuarioContextType = {
  usuario: Usuario;
  setUsuario: React.Dispatch<React.SetStateAction<Usuario>>;
};

const UsuarioContext = createContext<UsuarioContextType | undefined>(undefined);

export const UsuarioProvider = ({ children }: { children: ReactNode }) => {
  const [usuario, setUsuario] = useState<Usuario>(null);

  return (
    <UsuarioContext.Provider value={{ usuario, setUsuario }}>
      {children}
    </UsuarioContext.Provider>
  );
};

export const useUsuario = () => {
  const context = useContext(UsuarioContext);
  if (!context) throw new Error("useUsuario deve ser usado dentro de UsuarioProvider");
  return context;
};
```

---

### 2️⃣ `TelaUsuario.tsx`

```tsx
import React from "react";
import { useUsuario } from "../context/UsuarioContext";

export const TelaUsuario = () => {
  const { usuario, setUsuario } = useUsuario();

  return (
    <div style={{ padding: "20px" }}>
      {usuario ? <p>Olá, {usuario.nome}!</p> : <p>Nenhum usuário logado</p>}
      <button onClick={() => setUsuario({ nome: "João" })}>Login como João</button>
      <button
        onClick={() => setUsuario(null)}
        style={{ marginLeft: "10px", color: "red" }}
      >
        Logout
      </button>
    </div>
  );
};
```

---

### 3️⃣ `App.tsx` (usuário)

```tsx
import React from "react";
import { UsuarioProvider } from "./context/UsuarioContext";
import { TelaUsuario } from "./components/TelaUsuario";

export default function App() {
  return (
    <UsuarioProvider>
      <TelaUsuario />
    </UsuarioProvider>
  );
}
```

---

✅ Agora temos:

* Cada contexto em seu arquivo (`TemaContext.tsx` / `UsuarioContext.tsx`)
* Cada componente em seu próprio arquivo
* `App.tsx` apenas orquestrando os Providers e as telas
* Explicação clara sobre **contexto** e **prop drilling**


