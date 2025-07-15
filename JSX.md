JSX – A "Linguagem" do React

## O que é JSX?

**JSX** (JavaScript XML) é uma sintaxe especial usada no React que mistura **HTML com JavaScript**.  

Ela permite escrever a estrutura visual dos componentes React de forma parecida com HTML, mas dentro do JavaScript.

---

## Por que usar JSX?

- Facilita a criação de componentes visuais.
- Torna o código mais legível e intuitivo.
- É transformado pelo React em chamadas JavaScript que criam elementos para a página.

---

## Exemplo básico de JSX:

```jsx
const elemento = <h1>Olá, mundo!</h1>;
````

---

## 🚨 Regras importantes do JSX

### 1. **Só pode ter um elemento pai**

Todo JSX deve estar dentro de **um único elemento pai**.

**Errado:**

```jsx
return (
  <h1>Olá</h1>
  <p>Seja bem-vindo!</p>
);
```

**Correto:**

```jsx
return (
  <div>
    <h1>Olá</h1>
    <p>Seja bem-vindo!</p>
  </div>
);
```

Ou pode usar um **fragmento** (elemento vazio) para não criar uma `div` extra:

```jsx
return (
  <>
    <h1>Olá</h1>
    <p>Seja bem-vindo!</p>
  </>
);
```

---

### 2. **Use `className` em vez de `class`**

No HTML usamos `class` para definir classes CSS.
No JSX, por causa do JavaScript, usamos **`className`**.

```jsx
// Errado:
<div class="container"></div>

// Certo:
<div className="container"></div>
```

---

### 3. **Sempre feche as tags**

Todas as tags em JSX devem estar fechadas, mesmo as que são auto-fechadas no HTML.

```jsx
// Errado:
<br>

// Certo:
<br />

// Também correto:
<input type="text" />
```

---

### 4. **Atributos seguem camelCase**

Alguns atributos HTML que são múltiplas palavras, no JSX são camelCase:

| HTML      | JSX       |
| --------- | --------- |
| tabindex  | tabIndex  |
| onclick   | onClick   |
| maxlength | maxLength |

Exemplo:

```jsx
<button onClick={minhaFuncao}>Clique aqui</button>
```

---

## Inserindo variáveis e expressões no JSX

Você pode colocar **variáveis** e **qualquer código JavaScript válido** dentro de JSX usando **chaves `{}`**.

### Exemplo com variável:

```jsx
const nome = "Maria";

return <h1>Olá, {nome}!</h1>;
```

Isso vai renderizar:

```
Olá, Maria!
```

---

### Exemplo com expressões:

```jsx
const a = 5;
const b = 10;

return <p>5 + 10 = {a + b}</p>;
```

Renderiza:

```
5 + 10 = 15
```

---

### Usando funções dentro do JSX

Você pode chamar funções dentro das chaves também:

```jsx
function cumprimentar() {
  return "Olá!";
}

return <h1>{cumprimentar()}</h1>;
```

---

### Condicional no JSX

Pode usar operadores ternários dentro das chaves para mostrar algo condicionalmente:

```jsx
const estaLogado = true;

return (
  <div>
    {estaLogado ? <p>Bem-vindo!</p> : <p>Por favor, faça login.</p>}
  </div>
);
```

---

## Resumo das principais regras do JSX

| Regra                           | Descrição                           | Exemplo                            |
| ------------------------------- | ----------------------------------- | ---------------------------------- |
| Um único elemento pai           | Todo JSX precisa de um elemento pai | `<div>...</div>` ou `<>...</>`     |
| Usar `className`                | Para classes CSS, não `class`       | `<div className="meu-estilo">`     |
| Tags sempre fechadas            | Mesmo tags auto-fechadas            | `<img />`, `<input />`, `<br />`   |
| Atributos em camelCase          | Eventos e atributos                 | `onClick`, `tabIndex`, `maxLength` |
| Variáveis e expressões com `{}` | Inserir JS no JSX                   | `{nome}`, `{a + b}`, `{função()}`  |

---

## Exemplos completos

```jsx
function MeuComponente() {
  const nome = "Carlos";
  const idade = 25;

  return (
    <div className="perfil">
      <h1>Olá, {nome}!</h1>
      <p>Você tem {idade} anos.</p>
      <button onClick={() => alert("Clicou!")}>Clique aqui</button>
    </div>
  );
}
```
