# React + TypeScript + Vite

> **Environment prerequisites**
> - Node.js **v20.19.0+ (recommended >=22.12.0)** – this project uses Vite which warns on earlier versions.
> - On Windows, you can use the portable build unpacked under `C:\nodejs` and update your PATH accordingly.
> - A relaxed PowerShell execution policy may be required for some NPM scripts; see below.


This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) (or [oxc](https://oxc.rs) when used in [rolldown-vite](https://vite.dev/guide/rolldown)) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Running the project

### Deploying to GitHub Pages

1. Set the `homepage` field in `package.json` (replace `<USERNAME>` and `<REPO>` with your GitHub
   username and repository name).
2. Configure `vite.config.ts` with the correct base path according to the repo:

   ```ts
   export default defineConfig({
     base: process.env.NODE_ENV === 'production' ? '/<REPO>/' : './',
     plugins: [react()],
     resolve: {
       alias: {
         "@": path.resolve(__dirname, "./src"),
       },
     },
   });
   ```

3. Build and push the output:

   ```bash
   npm run build
   # commit and push the contents of dist/ to the gh-pages branch
   # you can use the gh-pages package or GitHub Actions to automate this
   ```

4. In your repository settings, enable GitHub Pages and point it at the `gh-pages` branch or
   `docs/` folder as appropriate.

If the base path isn’t correct, the site will 404 or show blank when hosted on GitHub Pages.  
See https://vitejs.dev/guide/static-deploy.html#github-pages for more details.

## React Compiler

A helper script `run-dev.bat` is included to launch the development server on Windows. It updates the PATH to include the portable Node.js installation and avoids PowerShell execution policy problems:

```bat
@echo off
set PATH=C:\nodejs\node-v22.12.0-win-x64;%PATH%
cd /d "C:\Users\USER\Downloads\wilmer cons\app"
call npm run dev
pause
```

You can also run:

```bash
# from a shell where `node` is available in PATH
npm install
npm run dev
```

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Other configs...

      // Remove tseslint.configs.recommended and replace with this
      tseslint.configs.recommendedTypeChecked,
      // Alternatively, use this for stricter rules
      tseslint.configs.strictTypeChecked,
      // Optionally, add this for stylistic rules
      tseslint.configs.stylisticTypeChecked,

      // Other configs...
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
])
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Other configs...
      // Enable lint rules for React
      reactX.configs['recommended-typescript'],
      // Enable lint rules for React DOM
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
])
```
