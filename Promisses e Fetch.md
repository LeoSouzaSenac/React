# 📦 Promises e fetch() no JavaScript

## ✨ O que é uma Promise?

Em JavaScript, uma **Promise** (promessa) é um jeito de **trabalhar com tarefas que demoram um tempo para acontecer**, como buscar dados de um servidor.

Em vez de bloquear o código até a tarefa terminar, a Promise **espera a resposta** e te avisa quando estiver pronta — ou quando der erro.

---

## 🔁 Exemplo da vida real

Imagine que você peça uma pizza pelo celular. A pizzaria diz: "Vamos te avisar quando estiver pronta."

Isso é uma Promise:

- 📦 Pedido feito → Promise criada
- ✅ Pizza chegou → **Resolve (sucesso)**
- ❌ Erro na entrega → **Reject (falha)**

---

## 🔨 Criando uma Promise

```js
const promessa = new Promise((resolve, reject) => {
  const sucesso = true;

  if (sucesso) {
    resolve("Deu certo!");
  } else {
    reject("Deu erro!");
  }
});
````

### Usando `.then()` e `.catch()` para lidar com o resultado:

```js
promessa
  .then(resposta => {
    console.log(resposta); // Deu certo!
  })
  .catch(erro => {
    console.log(erro); // Deu erro!
  });
```

---

## 🌐 O que é `fetch()`?

O `fetch()` é uma **função do JavaScript que usa Promises** para **fazer requisições HTTP** — ou seja, buscar dados da internet (geralmente de uma API).

### Sintaxe básica:

```js
fetch("https://api.exemplo.com/dados")
  .then(resposta => resposta.json()) // Converte para JSON
  .then(dados => {
    console.log(dados); // Usa os dados recebidos
  })
  .catch(erro => {
    console.log("Erro:", erro);
  });
```

---

## 📦 Explicando passo a passo:

1. **fetch(url)** faz a requisição.
2. O `then(resposta => resposta.json())` transforma a resposta em JSON (formato de dados).
3. O próximo `then(dados => { ... })` é onde você usa os dados.
4. O `catch(erro => { ... })` trata qualquer erro que acontecer.

---

## ✅ Exemplo real com API pública

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then(res => res.json())
  .then(usuarios => {
    usuarios.forEach(usuario => {
      console.log(usuario.name);
    });
  })
  .catch(erro => console.log("Erro ao buscar usuários:", erro));
```

---

## 🚀 Usando `async` e `await` (forma moderna)

Com `async` e `await`, você pode escrever código assíncrono de forma **mais parecida com código normal**.

### Exemplo:

```js
async function buscarUsuarios() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/users");
    const usuarios = await resposta.json();
    console.log(usuarios);
  } catch (erro) {
    console.log("Erro:", erro);
  }
}

buscarUsuarios();
```

## 🧠 O que são `async` e `await`?

### Resumo rápido:

* `async` → transforma uma função comum em uma função **assíncrona** (que trabalha com **Promises**).
* `await` → **espera** o resultado de uma Promise antes de continuar o código.

---

### 🔄 O problema com `.then()` e `.catch()`

Quando usamos apenas `.then()` e `.catch()`, o código pode ficar difícil de ler:

```js
fetch("https://api.com/dados")
  .then(res => res.json())
  .then(data => {
    console.log(data);
  })
  .catch(erro => {
    console.log("Erro:", erro);
  });
```

---

## ✅ Com `async` e `await`, fica mais limpo:

```js
async function buscarDados() {
  try {
    const resposta = await fetch("https://api.com/dados");
    const dados = await resposta.json();
    console.log(dados);
  } catch (erro) {
    console.log("Erro:", erro);
  }
}

buscarDados();
```

---

## 🔍 Explicando passo a passo

### 1. `async function`

Você coloca `async` na frente da função para dizer:

> "Essa função vai usar `await` e vai trabalhar com Promises."

```js
async function minhaFuncao() {
  // Pode usar await aqui dentro
}
```

---

### 2. `await`

Você usa `await` na frente de uma Promise para **esperar o resultado**.

```js
const resposta = await fetch("https://api.com/dados");
```

Esse código **espera** o `fetch()` terminar antes de continuar.

---

## 🧠 Por que usar `async/await`?

* Torna o código **mais fácil de ler e entender**
* Parece código "normal", mas funciona de forma assíncrona
* Ideal para **funções com várias etapas** que dependem de dados externos (como APIs)

---

## ⚠️ Importante:

Você **só pode usar `await` dentro de uma função `async`**.

Errado:

```js
const dados = await fetch("url"); // ❌ Vai dar erro fora de async
```

Correto:

```js
async function pegarDados() {
  const dados = await fetch("url"); // ✅
}
```

---

## 📦 Exemplo completo com tudo:

```js
async function carregarUsuarios() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/users");
    const usuarios = await resposta.json();
    usuarios.forEach(usuario => {
      console.log(usuario.name);
    });
  } catch (erro) {
    console.error("Erro ao buscar usuários:", erro);
  }
}

carregarUsuarios();
```
---

## 📌 Conclusão

* **Promises** ajudam a lidar com ações que demoram.
* **fetch()** é usado para buscar dados externos e **retorna uma Promise**.
* Você pode usar `.then()` / `.catch()` ou `async` / `await` para lidar com essas promessas.
* Essas ferramentas são essenciais quando se trabalha com **APIs e dados externos** — muito comum em aplicações web e React.

---

## 🧠 Dica

Sempre que for trabalhar com dados externos (por exemplo, buscar produtos, usuários ou posts de uma API), **você vai usar Promises e fetch!**


