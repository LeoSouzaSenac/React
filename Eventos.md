# React - Eventos

No React, eventos funcionam de forma muito parecida com o JavaScript tradicional, mas com algumas diferenças importantes na sintaxe e no comportamento.

---

## Como funcionam os eventos no React?

- Os eventos são escritos em **camelCase** (ex: `onClick`, `onChange`).
- Você passa uma **função** como handler, não uma string.
- Exemplo básico:

```jsx
<button onClick={handleClick}>Clique aqui</button>
````

---

## Principais eventos usados no React

### 1. `onClick`

* Disparado quando o usuário clica em um elemento.
* Muito usado em botões, links, divs clicáveis.

```jsx
<button onClick={() => alert('Clicou!')}>Clique</button>
```

---

### 2. `onChange`

* Disparado quando o valor de um input, select ou textarea muda.
* Essencial para formulários controlados.

```jsx
<input type="text" onChange={e => setValor(e.target.value)} />
```

---

### 3. `onSubmit`

* Usado em formulários, disparado quando o usuário envia o formulário.
* É comum prevenir o comportamento padrão para evitar o reload da página.

```jsx
<form onSubmit={handleSubmit}>
  ...
</form>

// Dentro do handleSubmit
function handleSubmit(e) {
  e.preventDefault();
  // processar os dados do formulário
}
```

---

### 4. `onMouseEnter` e `onMouseLeave`

* Disparados quando o mouse entra ou sai de um elemento.
* Úteis para efeitos visuais, tooltips etc.

```jsx
<div onMouseEnter={() => setHover(true)} onMouseLeave={() => setHover(false)}>
  Hover aqui
</div>
```

---

### 5. `onFocus` e `onBlur`

* `onFocus`: quando um elemento (input, textarea) ganha foco.
* `onBlur`: quando perde o foco.
* Muito usados para validação de formulários ou UI.

```jsx
<input onFocus={() => console.log('Focado')} onBlur={() => console.log('Saiu do foco')} />
```

---

### 6. `onKeyDown`, `onKeyPress`, `onKeyUp`

* Eventos relacionados ao teclado.
* Permitem detectar quando o usuário pressiona teclas.

```jsx
<input onKeyDown={e => console.log('Tecla pressionada:', e.key)} />
```

---

## Exemplo completo com vários eventos

```jsx
function Formulario() {
  const [nome, setNome] = React.useState('');
  const [mensagem, setMensagem] = React.useState('');
  
  function handleSubmit(e) {
    e.preventDefault();
    alert(`Nome: ${nome}\nMensagem: ${mensagem}`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={nome}
        onChange={e => setNome(e.target.value)}
        onFocus={() => console.log('Input nome focado')}
      />
      <textarea
        value={mensagem}
        onChange={e => setMensagem(e.target.value)}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## Observações importantes

* No React, **não é necessário usar `addEventListener`** para eventos normais.
* Para evitar o comportamento padrão de alguns eventos (como submit), use `event.preventDefault()`.
