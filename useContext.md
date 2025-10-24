
# ⚛️ React – Hook `useContext`

O **`useContext`** é um **hook que permite compartilhar dados entre componentes** sem precisar passar manualmente via props.
Ele é essencial para criar **estados globais** como:

* Tema claro/escuro
* Usuário logado
* Carrinho de compras
* Preferências do app

---

## 🧩 O que é *Prop Drilling*?

**Prop Drilling** é o problema que ocorre quando você precisa **passar dados de um componente pai para componentes profundamente aninhados** apenas para que eles possam usar esses dados.

Exemplo sem contexto:

```tsx
<App>
  <ComponentePai>
    <ComponenteFilho>
      <ComponenteNeto>
        <BotaoPrecisaDoDado />
      </ComponenteNeto>
    </ComponenteFilho>
  </ComponentePai>
</App>
```

Se o `BotaoPrecisaDoDado` precisa de um dado do `<App />`, você teria que **passar props por cada nível**, mesmo que os componentes intermediários **não usem o dado**. Isso é o *prop drilling*. 😵

O **`useContext`** resolve isso, permitindo que qualquer componente **consuma dados diretamente do contexto**, sem passar props manualmente.

---

## 🎬 Criando um Contexto – Tema Claro/Escuro

```tsx
// TemaContext.tsx
import React, { createContext, useState, useContext, ReactNode } from "react";

// 1️⃣ Criando o contexto
type TemaContextType = {
  temaEscuro: boolean;
  setTemaEscuro: React.Dispatch<React.SetStateAction<boolean>>;
};

const TemaContext = createContext<TemaContextType | undefined>(undefined);

// 2️⃣ Criando o Provider (componente que fornece os dados)
export const TemaProvider = ({ children }: { children: ReactNode }) => {
  const [temaEscuro, setTemaEscuro] = useState(false);

  return (
    <TemaContext.Provider value={{ temaEscuro, setTemaEscuro }}>
      {children}
    </TemaContext.Provider>
  );
};

// 3️⃣ Hook personalizado para consumir o contexto
export const useTema = () => {
  const context = useContext(TemaContext);
  if (!context) throw new Error("useTema deve ser usado dentro de TemaProvider");
  return context;
};
```

---

## ⚡ Exemplo prático: alternando tema claro/escuro

```tsx
// App.tsx
import React from "react";
import { TemaProvider, useTema } from "./TemaContext";

const ComponenteBotao = () => {
  const { temaEscuro, setTemaEscuro } = useTema();

  return (
    <button onClick={() => setTemaEscuro(!temaEscuro)}>
      {temaEscuro ? "Mudar para claro" : "Mudar para escuro"}
    </button>
  );
};

const Tela = () => {
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

export default function App() {
  return (
    <TemaProvider>
      <Tela />
    </TemaProvider>
  );
}
```

---

## 🔄 Exemplo 2 – Contexto de usuário logado

```tsx
// UsuarioContext.tsx
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

```tsx
// App.tsx
import React from "react";
import { UsuarioProvider, useUsuario } from "./UsuarioContext";

const TelaUsuario = () => {
  const { usuario, setUsuario } = useUsuario();

  return (
    <div style={{ padding: "20px" }}>
      {usuario ? <p>Olá, {usuario.nome}!</p> : <p>Nenhum usuário logado</p>}
      <button onClick={() => setUsuario({ nome: "João" })}>Login como João</button>
      <button onClick={() => setUsuario(null)} style={{ marginLeft: "10px", color: "red" }}>
        Logout
      </button>
    </div>
  );
};

export default function App() {
  return (
    <UsuarioProvider>
      <TelaUsuario />
    </UsuarioProvider>
  );
}
```

---

## ⚙️ Resumo rápido

| Conceito             | Explicação                                     |
| -------------------- | ---------------------------------------------- |
| Prop Drilling        | Passar props manualmente por vários níveis     |
| Contexto (`Context`) | Permite compartilhar dados globalmente         |
| Provider             | Componente que fornece os dados                |
| Consumer/Hook        | Componente que consome os dados (`useContext`) |

---

## 🧭 Conclusão

O `useContext` é essencial quando você quer:

* Evitar **prop drilling**
* Ter **estados globais** ou **configurações compartilhadas**
* Acessar e alterar dados de forma **limpa e direta**

> 🔹 `useState` = cria estados locais
> 🔹 `useEffect` = reage às mudanças
> 🔹 `useContext` = compartilha estados globalmente

---


Quer que eu faça?
