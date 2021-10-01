# React.JS + Typescript + ESlint + Prettier

Neste guia, vamos entender como iniciar uma aplicação React.JS utilizando o Typescript com os plugins do ESLint e Prettier. 

Essas configurações foram inspiradas pelo sistema de educação da Rocketseat 💜.

O npm deve estar instalado na máquina onde será iniciado o desenvolvimento desta aplicação. Versão 5.2+, para termos o recurso 'npx'.

Como o npm já é instalado junto com o Node.JS, provavelmente você já possui ele na sua máquina. Caso contrário basta efetuar a instalação do mesmo.

💚 Para a instalação do node acesse: [nodejs.org](https://nodejs.org/)

## Iniciando a aplicação React.JS + Typescript

Na pasta onde iremos iniciar a aplicação vamos digitar o seguinte comando:

```json
npx create-react-app nome-do-app --template=typescript
```

Dessa forma, o create-react-app irá gerar uma aplicação padrão já pré-configurada para o uso de typescript.

Uma coisa legal a se fazer de inicio seria a geração do arquivo ".editorconfig" clicando com o botão direito no explorer do VSCode e selecionando a opção "Generate .editorconfig" (necessita da extensão EditorConfig).

A configuração que podemos utilizar no .editorconfig seria:

```jsx
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

Essas configurações são as que mais me deixaram confortável no desenvolvimento, mas, não é uma regra absoluta 😆.

Agora vamos limpar a aplicação, para manter somente o que interessa e agilizar a nossa configuração.

Para isso, vamos excluir os seguintes arquivos:

```json
-- Pasta Public
favicon.ico
logo192.png
logo512.png
manifest.json

-- Pasta src
App.css
App.test.tsx
index.css
logo.svg
reportWebVitals.ts
setupTests.ts
README.md
```

Agora, nos arquivos public/index.html, src/App.tsx e src/index.tsx vamos remover as declarações dos arquivos removidos acima.

Por fim, estes arquivos ficarão como os exemplos abaixo:

public/index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

src/App.tsx

```jsx
import React from 'react';

function App() {
  return <h1>Hello Galaxy!</h1>;
}

export default App;
```

src/index.tsx

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

E ao iniciar com o comando 'yarn start' vamos obter o seguinte resultado

![Untitled](React%20JS%20+%20Typescript%20+%20ESlint%20+%20Prettier%20f6ee2e32ed8147cdafdda089f204f13b/Untitled.png)

## Instalando e configurando ESLint

Vamos adicionar o ESLint como uma dependência de desenvolvimento através do comando:

```json
yarn add eslint -D
```

Em seguida precisamos iniciar o ESLint para definirmos as preferências de lint do nosso projeto:

```json
yarn eslint --init
```

Ao executar este comando, vamos responder algumas questões para a configuração do ESLint no projeto. Essas são as configurações que estou utilizando no momento:

**"How would you like to use ESLint?"**

= To check syntax, find problem, and enforce code style

**"What type of modules does your project use?"**

= JavaScript modules (import/export)

**"Wich framework does your project use?"**

= React

**"Does your project use typescript?"**

= Yes

**"Where does your code run?"**

= Browser.

**"How would you like to define a style for your project?"**

= Use a popular style guide.

= Arbnb...

**"What format do you want your config file to be in?"**

= JSON

Em seguida serão listados alguns recursos que devem ser instalados além do ESLint e em seguida  a seguinte pergunta:

**"Would you like to install them with npm?"**

= YES

> Caso queira, você pode fazer a instalação via yarn. Basta copiar exatamente as dependências listadas e instalar com o comando.
> 

Vamos adicionar uma dependência de desenvolvimento do ESLint, que gerencia as importações no Typescript, que pode ser adicionada com o seguinte comando:

```json
yarn add eslint-import-resolver-typescript -D
```

Observação: a extensão do ESLint deve estar instalada e habilitada no VSCode.

O arquivo 'eslintrc.json' que define as opções e regras do ESLint deve estar como o exemplo abaixo: 

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "plugin:react/recommended",
    "airbnb",
    "plugin:@typescript-eslint/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["react", "@typescript-eslint", "react-hooks"],
  "rules": {
    "no-use-before-define": "off",
    "@typescript-eslint/no-use-before-define": ["error"],
    "react/jsx-filename-extension": ["warn", { "extensions": [".tsx"] }],
    "@typescript-eslint/explicit-function-return-type": [
      "error",
      {
        "allowExpressions": true
      }
    ],
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "ts": "never",
        "tsx": "never"
      }
    ],
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "import/prefer-default-export": "off",
    "react/prop-types": "off",
    "react/jsx-no-bind": ["warn",{
      "ignoreDOMComponents": true
    }],
    "camelcase": "off"
  },
  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
}
```

Neste momento, os arquivos App.tsx e index.tsx podem apresentar alguns erros de sintax (ESLint funcionando "uhuuuul \o/". Por isso vamos adequar os códigos destes arquivos para:

src/App.tsx

```jsx
import React from 'react';

const App: React.FC = () => <h1>Hello Galaxy!</h1>;

export default App;
```

src/index.tsx

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root'),
);
```

Vamos então, criar o arquivo ".eslintignore" na raiz do nosso projeto, com o seguinte conteúdo:

```json
/*.js
node_modules
dist
```

O esperado é que a mensagem 'Compiled successfully!' seja retornada no terminal caso o servidor local esteja sendo executado 🤓. Nos aqruivos, o esperado é que não tenha mais erros do ESLint.

## Instalando e configurando o Prettier

Vamos então adicionar o Prettier e os demais recursos para a integração do Prettier com o ESLint. Para isso vamos executar o seguinte comando:

```json
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

Ao finalizar a instalação dessas dependências no nosso projeto, vamos começar a configurar nossas preferências para estes plugins. 

O que será descrito abaixo não são regras absolutas mas é o que mais funciona para grande parte dos usuários...

Vamos iniciar a configuração adicionando algumas orientações no arquivo ".eslintrc.json". Por fim o arquivo deve ser parecido com isso:

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "plugin:react/recommended",
    "airbnb",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["react", "@typescript-eslint", "react-hooks", "prettier"],
  "rules": {
    "prettier/prettier": "error",
    "no-use-before-define": "off",
    "@typescript-eslint/no-use-before-define": ["error"],
    "react/jsx-filename-extension": ["warn", { "extensions": [".tsx"] }],
    "@typescript-eslint/explicit-function-return-type": [
      "error",
      {
        "allowExpressions": true
      }
    ],
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "ts": "never",
        "tsx": "never"
      }
    ],
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "import/prefer-default-export": "off",
    "react/prop-types": "off",
    "react/jsx-no-bind": ["warn",{
      "ignoreDOMComponents": true
    }],
    "camelcase": "off"
  },
  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
}
```

Vamos agora, criar o arquivo "prettier.config.js" na raiz do nosso projeto, com o seguinte código:

```json
module.exports = {
	singleQuote: true,
	trailingComma: "all",
	arrowParens: "avoid"
}
```

Observações: 

- Assim como o ESLint, o Prettier também precisa da sua extensão instalada e habilitada no VSCode;
- Caso alguma função não estiver funcionando como o esperado, é recomendado reiniciar o VSCode para que seja carregada novamente a IDE e seus recursos.

Agora já estamos prontos para o desenvolvimento com React.JS, utilizando o template Typescript com o ESLInt e Prettier 🚀.