# react-vite

react + vite + typescript 설정해보기

## 설정 방법

### react 설치

```zsh
yarn add react react-dom react-router-dom
```

### typescript 설치

````zsh
yarn add -D typescript @types/react @types/react-dom```
````

### tsconfig.json 설정

```zsh
npx tsc --init
```

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "moduleResolution": "bundler",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true,
    "allowJs": false,
    "jsx": "react-jsx",

    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src", "vite.config.js"],
  "exclude": ["node_modules", "build", "dist"]
}
```

### vite 설치

```zsh
yarn add -D vite @vitejs/plugin-react
```

### vite.config.js 파일 생성 및 수정

```javascript
import react from '@vitejs/plugin-react';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': '/src',
    },
  },
});
```

### index.html 파일 생성

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React-vite</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/index.tsx"></script>
  </body>
</html>
```

### /src 경로에 index.tsx , App.tsx 생성

```tsx
// index.tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from '@/App';

const rootNode = document.getElementById('root') as HTMLElement;

ReactDOM.createRoot(rootNode).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
);
```

```tsx
// App.tsx
import React from 'react';

function App() {
  return <div>Hello React-Vite !</div>;
}

export default App;
```

### Prettier 설치 및 .prettierrc 설정

```json
// .prettierrc
{
  "printWidth": 100,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "arrowParens": "always",
  "quoteProps": "preserve",
  "trailingComma": "all",
  "jsxBracketSameLine": true,
  "bracketSpacing": true
}
```

### ESLint 설치 및 .eslintrc 설정

```zsh
yarn add -D eslint
npx eslint --init
```

```json
// .eslintrc
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "project": "./tsconfig.json",
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "ignorePatterns": ["dist/", "node_modules/"],
  "plugins": ["@typescript-eslint", "react"],
  "rules": {
    "react/react-in-jsx-scope": "off"
  }
}
```

### package.json srcript 추가

```json
{
  //...
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
  //...
}
```
