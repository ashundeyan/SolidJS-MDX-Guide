# How to Actually Install MDX on SolidJS

The official guide is pretty horrific. Despite what the SolidJS Ecosystem may suggest, you only need the official project. Here's how you actually do it.

- **Step 1:** Install MDX for Rollup in a new SolidJS project:  
    ```bash
    npm install @mdx-js/rollup
    ```

- **Step 2:** If using TypeScript, install the types:  
    ```bash
    npm install @types/mdx --save-dev
    ```

- **Step 3:** Add the MDX types to your `tsconfig.json`:  
  - `tsconfig.json`  
    ```json
    {
      "compilerOptions": {
        "strict": true,
        "target": "ESNext",
        "module": "ESNext",
        "moduleResolution": "node",
        "allowSyntheticDefaultImports": true,
        "esModuleInterop": true,
        "jsx": "preserve",
        "jsxImportSource": "solid-js",
        "types": [
          "vite/client",
          "mdx"
        ],
        "noEmit": true,
        "isolatedModules": true
      }
    }
    ```

- **Step 4:** Add MDX to your Vite config:  
  - `vite.config.ts`  
    ```ts
    import { defineConfig } from 'vite';
    import mdx from '@mdx-js/rollup'
    import solidPlugin from 'vite-plugin-solid';

    export default defineConfig({
      plugins: [
        solidPlugin(),
        mdx({
          jsxImportSource: 'solid-js/h'
        })
      ],
      server: {
        port: 3000,
      },
      build: {
        target: 'esnext',
      },
    });
    ```

- **Step 5:** Import and/or render your MDX:  
  - `index.ts`  
    ```ts
    /* @refresh reload */
    import { render } from 'solid-js/web';

    import './index.css';
    import MyMdx from './MyMdx.mdx'
    const root = document.getElementById('root');

    render(() => <MyMdx />, root!);
    ```

That's it!
