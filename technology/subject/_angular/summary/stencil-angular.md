Stencil is a compiler for building fast web apps using Web Components. It generates standards-based Web Components, while still delivering the benefits of a modern JavaScript framework, such as reactive data-binding and a declarative component style. Here's a step-by-step guide to installing Stencil and creating a basic component:

### Step 1: Install Node.js and npm
Ensure you have Node.js and npm installed on your system. You can download and install them from the [Node.js website](https://nodejs.org/).

### Step 2: Create a New Stencil Project
Use npm to create a new Stencil project. Open your terminal and run:

```sh
npm init stencil
```

You will be prompted to choose a project type. For this example, select `component` (or any other type if preferred).

### Step 3: Navigate to Your Project Directory
Change to the directory of your newly created project:

```sh
cd my-stencil-project
```

### Step 4: Install Dependencies
Install the necessary dependencies by running:

```sh
npm install
```

### Step 5: Start the Development Server
Start the Stencil development server to begin developing your component:

```sh
npm start
```

This command will start a local development server and open your default web browser to `http://localhost:3333`.

### Step 6: Create a New Component
To create a new component, run the following command:

```sh
npm run generate
```

You will be prompted to enter the tag name for your new component (e.g., `my-component`).

### Step 7: Edit Your Component
Navigate to the `src/components/my-component` directory and open `my-component.tsx`. This is where you define your component. Here’s a simple example:

```tsx
import { Component, Prop, h } from '@stencil/core';

@Component({
  tag: 'my-component',
  styleUrl: 'my-component.css',
  shadow: true
})
export class MyComponent {
  @Prop() name: string;

  render() {
    return (
      <div>
        <p>Hello, {this.name}!</p>
      </div>
    );
  }
}
```

In this example, the component has a single property (`name`) that is displayed in a paragraph element.

### Step 8: Add Styles to Your Component
Open `my-component.css` in the same directory and add some styles for your component:

```css
:host {
  display: block;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

p {
  font-size: 20px;
  color: #333;
}
```

### Step 9: Use Your Component
To use your new component, you can include it in the `src/index.html` file or any other HTML file within your project:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Stencil Component Example</title>
  </head>
  <body>
    <my-component name="Stencil"></my-component>

    <script type="module" src="/build/my-stencil-project.esm.js"></script>
    <script nomodule src="/build/my-stencil-project.js"></script>
  </body>
</html>
```

### Step 10: Build Your Project for Production
When you are ready to build your project for production, run:

```sh
npm run build
```

This command will create a `www` directory with the compiled files that can be deployed to a web server.

### Step 11: Deploy Your Project
You can deploy the contents of the `www` directory to any static web hosting service (e.g., GitHub Pages, Netlify, Vercel, etc.).

### Conclusion
You now have a basic understanding of how to install and create components using Stencil. This setup allows you to build reusable, standards-based web components with ease. Stencil's approach makes it a powerful tool for modern web development, providing the benefits of a framework without the overhead.


-----


To include a Stencil-built component library in an Angular project, follow these steps:

### 1. Build the Stencil Component Library

First, ensure your Stencil components are built and ready to be included in other projects. Run the build command in your Stencil project:

```sh
npm run build
```

This will generate the compiled components in the `dist` directory.

### 2. Install the Component Library in the Angular Project

If your Stencil component library is published as an npm package, you can install it directly. Otherwise, you can link it locally.

#### Option A: Install from npm

If the library is published to npm:

```sh
npm install your-stencil-library
```

#### Option B: Link Locally

If the library is local:

1. In the Stencil project directory, create a symbolic link:

    ```sh
    npm link
    ```

2. In your Angular project directory, link the Stencil library:

    ```sh
    npm link your-stencil-library
    ```

### 3. Integrate the Stencil Components in the Angular Project

Follow these steps to use the Stencil components in your Angular project.

#### Step 1: Modify `angular.json`

Ensure Angular knows to process custom elements:

1. Open `angular.json`.
2. Add the following to the `architect > build > options` and `architect > test > options` sections:

    ```json
    "scripts": [
      "node_modules/your-stencil-library/dist/your-stencil-library/your-stencil-library.esm.js",
      "node_modules/your-stencil-library/dist/your-stencil-library/your-stencil-library.js"
    ]
    ```

#### Step 2: Modify `tsconfig.json`

Make sure TypeScript recognizes the custom elements:

1. Open `tsconfig.json`.
2. Add the following to the `compilerOptions`:

    ```json
    "types": [
      "your-stencil-library"
    ]
    ```

#### Step 3: Modify `main.ts`

Add the following code to `src/main.ts` to import the components and define custom elements:

```ts
import { defineCustomElements } from 'your-stencil-library/loader';

defineCustomElements(window);
```

#### Step 4: Use Stencil Components in Angular Templates

Now, you can use the Stencil components in your Angular templates like any other HTML element.

1. In an Angular component HTML file (e.g., `app.component.html`), add the Stencil component:

    ```html
    <my-stencil-component></my-stencil-component>
    ```

2. If your Stencil component uses any attributes or properties, pass them as you would with any other HTML element:

    ```html
    <my-stencil-component prop="value"></my-stencil-component>
    ```

### 4. Add Types for Stencil Components

To get type support for Stencil components in Angular, follow these steps:

1. Open or create a `custom-elements.d.ts` file in your Angular project's `src` directory.
2. Add the following code to the file:

    ```ts
    declare module 'your-stencil-library' {
      export * from 'your-stencil-library/dist/types/components';
    }
    ```

3. Add this file to the `files` array in your `tsconfig.app.json` file:

    ```json
    {
      "compilerOptions": {
        ...
      },
      "files": [
        "src/custom-elements.d.ts"
      ],
      ...
    }
    ```

### Example

Here is a simple example of integrating a Stencil component named `my-stencil-component`:

1. **Stencil Project**: Build the Stencil project:

    ```sh
    npm run build
    ```

2. **Angular Project**:

    - **Install the Stencil library**:

      ```sh
      npm install your-stencil-library
      ```

    - **Modify `angular.json`**:

      ```json
      "scripts": [
        "node_modules/your-stencil-library/dist/your-stencil-library/your-stencil-library.esm.js",
        "node_modules/your-stencil-library/dist/your-stencil-library/your-stencil-library.js"
      ]
      ```

    - **Modify `tsconfig.json`**:

      ```json
      "types": [
        "your-stencil-library"
      ]
      ```

    - **Modify `src/main.ts`**:

      ```ts
      import { defineCustomElements } from 'your-stencil-library/loader';

      defineCustomElements(window);
      ```

    - **Use the Stencil component in `app.component.html`**:

      ```html
      <my-stencil-component></my-stencil-component>
      ```

By following these steps, you can integrate Stencil-built components into your Angular project seamlessly.