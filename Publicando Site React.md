# 📦 Como publicar projeto React com Vite no GitHub Pages

Este guia mostra como configurar e publicar um projeto React + Vite no **GitHub Pages**, usando como base o projeto `react-nomad`.

---

## ✅ Pré-requisitos

- Node.js e npm instalados
- Conta no GitHub
- Projeto criado com Vite (`npm create vite@latest`)
- Código versionado e publicado no GitHub

---

## 📁 Estrutura esperada

Seu projeto deve estar assim:

```

react-nomad/
├── src/
│   └── main.jsx
├── public/
├── package.json
├── vite.config.js

````

---

## 📄 O que é `package.json`?

O `package.json` é o arquivo de configuração principal de qualquer projeto Node.js (como React + Vite). Ele define:

- O nome, versão e tipo do projeto
- As dependências (bibliotecas que seu projeto usa)
- Os scripts que automatizam tarefas (como rodar ou publicar seu app)
- O campo `homepage`, que informa onde o site será hospedado

---

## 🚀 O que é Deploy?

**Deploy** é o processo de **publicar seu projeto na internet**, permitindo que qualquer pessoa acesse pelo navegador, por meio de um link. No caso do GitHub Pages, fazemos isso enviando a versão final do site para a branch `gh-pages`.

---

## ⚡ O que é o Vite?

**Vite** é uma ferramenta moderna para criar e rodar projetos como React de forma **rápida e eficiente**. Ele:
- Roda um servidor local para desenvolvimento
- Transforma seu código para JavaScript puro
- Gera arquivos otimizados na pasta `dist/` para publicação

---

## 📦 Por que usamos a pasta `dist`?

A pasta `dist/` contém a **versão final do seu site**, pronta para ser lida pelos navegadores. Seu código JSX e módulos são convertidos em JavaScript puro, com arquivos otimizados e leves.  
👉 **Nunca se publica o código-fonte diretamente, e sim a pasta `dist/`**.

---

## 1️⃣ `package.json` comentado

```jsonc
{
  // Nome do projeto
  "name": "trabalho-final",

  // Impede publicação automática no npm
  "private": true,

  // Versão do projeto
  "version": "0.0.0",

  // Permite usar import/export modernos
  "type": "module",

  // URL do site no GitHub Pages
  "homepage": "https://leosouzasenac.github.io/react-nomad",

  "scripts": {
    // Inicia o servidor local
    "dev": "vite",

    // Cria a pasta dist com a versão final
    "build": "vite build",

    // Visualiza a versão final localmente
    "preview": "vite preview",

    // Publica o conteúdo da dist no GitHub Pages
    "deploy": "gh-pages -d dist",

    // Verifica possíveis problemas no código
    "lint": "eslint ."
  },

  // Bibliotecas da aplicação
  "dependencies": {
    "bootstrap": "^5.3.7",
    "react": "^19.1.0",
    "react-dom": "^19.1.0",
    "react-icons": "^5.5.0",
    "swiper": "^11.2.10"
  },

  // Ferramentas de desenvolvimento
  "devDependencies": {
    "@eslint/js": "^9.30.1",
    "@types/react": "^19.1.8",
    "@types/react-dom": "^19.1.6",
    "@vitejs/plugin-react": "^4.6.0",
    "eslint": "^9.30.1",
    "eslint-plugin-react-hooks": "^5.2.0",
    "eslint-plugin-react-refresh": "^0.4.20",
    "globals": "^16.3.0",
    "vite": "^7.0.4",

    // Necessário para fazer deploy com GitHub Pages
    "gh-pages": "^6.0.0"
  }
}
````

---

## 2️⃣ `vite.config.js` comentado

```js
// vite.config.js

import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  // Caminho base do site (deve ser o nome do repositório)
  base: '/react-nomad/',
  plugins: [react()]
})
```

---

## 3️⃣ Instalando dependências

No terminal, rode:

```bash
npm install
```

---

## 4️⃣ Fazendo o build do projeto

```bash
npm run build
```

> Isso criará a pasta `dist/` com os arquivos finais otimizados, prontos para deploy.

---

## 5️⃣ Publicando no GitHub Pages

```bash
npm run deploy
```

> Esse comando envia os arquivos da pasta `dist` para a branch `gh-pages` no seu repositório.

---

## 6️⃣ Ativando o GitHub Pages

1. Acesse seu repositório no GitHub
2. Vá em **Settings > Pages**
3. Em **Branch**, selecione `gh-pages`
4. Clique em **Save**

---

## ✅ Pronto!

Agora seu projeto está disponível em:

```
https://leosouzasenac.github.io/react-nomad/
```

---

## 🧠 Observações

* Sempre que fizer mudanças no código, **rode os comandos abaixo para atualizar o site:**

```bash
npm run build
npm run deploy
```

* Se estiver usando **React Router**, use `HashRouter` no lugar de `BrowserRouter` para evitar erros 404 em páginas internas.

---

## 💬 Testando localmente

Para testar a versão final antes do deploy, use:

```bash
npm run preview
```

---

## ✨ Dica extra: Deploy alternativo no Vercel

1. Acesse [https://vercel.com](https://vercel.com)
2. Faça login com sua conta GitHub
3. Clique em "Add New Project" e selecione seu repositório
4. Aceite as configurações padrão (Vite será detectado automaticamente)
5. Clique em **Deploy**

Seu site estará disponível em um domínio gratuito `.vercel.app`!
