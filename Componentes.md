# Componentes em React

---

## O que é um componente?

Um **componente** é uma **parte reutilizável da interface** do seu aplicativo React.  
Ele pode ser uma parte pequena, como um botão, ou uma parte maior, como um formulário ou uma página inteira.

### Por que usar componentes?

- Facilita organizar e dividir o código.
- Permite reutilizar partes do código em vários lugares.
- Torna o código mais fácil de manter e entender.

---

## Como criar um componente com função

Em React, a forma mais comum de criar componentes é usando **funções** que retornam JSX.

### Exemplo simples:

```jsx
function Saudacao() {
  return <h1>Olá, mundo!</h1>;
}
````

Para usar o componente:

```jsx
<Saudacao />
```

---

## Passar e receber props (propriedades)

**Props** são os dados que você passa para um componente para personalizá-lo.

### Exemplo:

```jsx
function Saudacao(props) {
  return <h1>Olá, {props.nome}!</h1>;
}
```

Usando o componente e passando a prop `nome`:

```jsx
<Saudacao nome="Maria" />
```

Resultado:

```
Olá, Maria!
```

---

### Usando desestruturação para pegar props

Em vez de usar `props.nome`, você pode desestruturar diretamente no parâmetro da função:

```jsx
function Saudacao({ nome }) {
  return <h1>Olá, {nome}!</h1>;
}
```

---

## Reutilização de componentes

Um dos grandes benefícios do React é a **reutilização**.

Você cria um componente uma vez e usa várias vezes, passando props diferentes para personalizar.

### Exemplo:

```jsx
function Botao({ texto, onClick }) {
  return <button onClick={onClick}>{texto}</button>;
}

// Usando o Botão em vários lugares
function App() {
  return (
    <div>
      <Botao texto="Salvar" onClick={() => alert("Salvo!")} />
      <Botao texto="Cancelar" onClick={() => alert("Cancelado!")} />
    </div>
  );
}
```

---

## Componentes podem ser aninhados

Um componente pode usar outros componentes dentro dele.

```jsx
function Perfil({ nome, idade }) {
  return (
    <div>
      <Saudacao nome={nome} />
      <p>Idade: {idade}</p>
    </div>
  );
}

function App() {
  return <Perfil nome="Carlos" idade={28} />;
}
```

---

## Resumo rápido

| Conceito          | Descrição                                                 |
| ----------------- | --------------------------------------------------------- |
| Componente        | Bloco reutilizável de interface em React                  |
| Função componente | Função que retorna JSX para exibir na tela                |
| Props             | Dados passados para personalizar componentes              |
| Reutilização      | Usar o mesmo componente várias vezes com props diferentes |
| Aninhamento       | Componentes dentro de componentes                         |

---

## Exemplo completo

```jsx
function Botao({ texto, onClick }) {
  return <button onClick={onClick}>{texto}</button>;
}

function Saudacao({ nome }) {
  return <h1>Olá, {nome}!</h1>;
}

function Perfil({ nome, idade }) {
  return (
    <div>
      <Saudacao nome={nome} />
      <p>Idade: {idade}</p>
      <Botao texto="Enviar mensagem" onClick={() => alert(`Mensagem enviada para ${nome}`)} />
    </div>
  );
}

function App() {
  return <Perfil nome="Ana" idade={22} />;
}
```
