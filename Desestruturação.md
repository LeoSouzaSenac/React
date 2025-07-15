# 📘 Desestruturação em JavaScript (Destructuring)

A **desestruturação** em JavaScript é uma forma de extrair valores de objetos ou arrays e atribuí-los a variáveis de forma mais prática e limpa.

---

## 🧠 Conceito Básico

Em vez de acessar as propriedades de um objeto uma por uma, você pode extrair diretamente:

### Exemplo tradicional:
```js
const pessoa = {
  nome: "João",
  idade: 30,
  cidade: "São Paulo"
};

const nome = pessoa.nome;
console.log(nome); // João
````

### Com desestruturação:

```js
const { nome } = pessoa;
console.log(nome); // João
```

---

## 🛠️ Como funciona?

Você indica quais propriedades deseja extrair e o JavaScript cria variáveis com esses nomes:

```js
const { nome, idade } = pessoa;
console.log(nome); // João
console.log(idade); // 30
```

---

## ✏️ Renomeando variáveis

Você pode dar um novo nome à variável usando `:`:

```js
const { nome: nomeUsuario } = pessoa;
console.log(nomeUsuario); // João
```

---

## 🧩 Valores padrão

Caso uma propriedade não exista no objeto, você pode definir um valor padrão:

```js
const { profissao = "Desconhecida" } = pessoa;
console.log(profissao); // Desconhecida
```

---

## 🧪 Usando em funções

Você pode aplicar desestruturação diretamente nos parâmetros da função:

```js
function exibir({ nome, cidade }) {
  console.log(`${nome} mora em ${cidade}`);
}

exibir(pessoa); // João mora em São Paulo
```

---

## ✅ Vantagens da Desestruturação

* Código mais limpo e legível
* Menos repetição
* Ideal para funções e manipulação de dados

---

## 📌 Conclusão

A desestruturação é uma ferramenta poderosa no JavaScript moderno, especialmente útil quando você trabalha com objetos grandes ou precisa tornar seu código mais enxuto.
