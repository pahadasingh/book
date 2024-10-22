Server-Side Rendering (SSR) in Angular involves rendering the application on the server and sending the fully rendered HTML to the client. This can significantly improve the performance and SEO of your Angular application, especially for the initial page load. Here's an overview of how SSR works in Angular, including key concepts and steps to implement it.

### Key Concepts

1. **Universal:** Angular Universal is a technology that allows Angular applications to be run on the server. It enables SSR by pre-rendering the application on the server side.
2. **Node.js:** Typically, a Node.js server is used to run the Angular application on the server.
3. **Angular CLI Support:** Angular CLI provides built-in support for setting up and building Universal applications.

### Benefits of SSR

- **Improved Performance:** Faster initial load times, as the server sends a fully rendered page to the client.
- **Better SEO:** Search engines can crawl the fully rendered HTML content, improving the discoverability and ranking of your application.
- **Enhanced User Experience:** Users see the content quicker, leading to a better perceived performance.

### How SSR Works in Angular

1. **Rendering on the Server:**
   - When a user requests a page, the Angular application is executed on the server. The server processes the request, runs the Angular application, and generates the HTML content.

2. **Sending Pre-rendered HTML:**
   - The server sends the fully rendered HTML to the client. The client sees the content immediately without waiting for the JavaScript to load and render the application.

3. **Hydration:**
   - Once the client receives the HTML, the Angular framework takes over. This process, called hydration, involves attaching Angular’s JavaScript functionality to the already rendered HTML. This makes the application interactive.

### Steps to Implement SSR in Angular

#### 1. Set Up Angular Universal

1. **Add Angular Universal to Your Project:**
   - Use the Angular CLI to add Angular Universal to your existing Angular project.
     ```sh
     ng add @nguniversal/express-engine
     ```

2. **Install Dependencies:**
   - The command above installs necessary dependencies and creates files required for SSR, including a server module and server-side entry point.

#### 2. Modify Server Module

- The `app.server.module.ts` file is created. This file contains the server-specific configuration for your Angular application.

#### 3. Configure the Server

- An Express server is typically used to handle requests and render the Angular application on the server. The `server.ts` file is created to configure the Express server.

  ```typescript
  import 'zone.js/node';
  import { ngExpressEngine } from '@nguniversal/express-engine';
  import * as express from 'express';
  import { join } from 'path';

  import { AppServerModule } from './src/main.server';
  import { APP_BASE_HREF } from '@angular/common';
  import { existsSync } from 'fs';

  // The Express app is exported so that it can be used by serverless Functions.
  export function app(): express.Express {
    const server = express();
    const distFolder = join(process.cwd(), 'dist/your-app-name/browser');
    const indexHtml = existsSync(join(distFolder, 'index.original.html')) ? 'index.original.html' : 'index';

    // Our Universal express-engine (found @ `@nguniversal/express-engine`)
    server.engine('html', ngExpressEngine({
      bootstrap: AppServerModule,
    }));

    server.set('view engine', 'html');
    server.set('views', distFolder);

    // Serve static files from /browser
    server.get('*.*', express.static(distFolder, {
      maxAge: '1y'
    }));

    // All regular routes use the Universal engine
    server.get('*', (req, res) => {
      res.render(indexHtml, { req, providers: [{ provide: APP_BASE_HREF, useValue: req.baseUrl }] });
    });

    return server;
  }

  function run(): void {
    const port = process.env.PORT || 4000;

    // Start up the Node server
    const server = app();
    server.listen(port, () => {
      console.log(`Node Express server listening on http://localhost:${port}`);
    });
  }

  // Webpack will replace 'require' with '__webpack_require__'
  // '__non_webpack_require__' is a proxy to Node 'require'
  // The below code is to ensure that the server is started only when not in unit test or e2e environment
  declare const __non_webpack_require__: NodeRequire;
  const mainModule = __non_webpack_require__.main;
  const moduleFilename = mainModule && mainModule.filename || '';
  if (moduleFilename === __filename || moduleFilename.includes('iisnode')) {
    run();
  }

  export * from './src/main.server';
  ```

#### 4. Update Angular Configuration

- Modify `angular.json` to include the server build and output configuration.

  ```json
  {
    ...
    "projects": {
      "your-app-name": {
        ...
        "architect": {
          "build": {
            ...
          },
          "server": {
            "builder": "@angular-devkit/build-angular:server",
            "options": {
              "outputPath": "dist/your-app-name/server",
              "main": "src/main.server.ts",
              "tsConfig": "tsconfig.server.json"
            }
          }
        }
      }
    }
  }
  ```

#### 5. Build and Serve the Application

1. **Build the Client and Server Bundles:**
   - Build the Angular application for both client and server.
     ```sh
     npm run build:ssr
     ```

2. **Serve the Application:**
   - Start the server to handle SSR.
     ```sh
     npm run serve:ssr
     ```

### Conclusion

SSR in Angular, facilitated by Angular Universal, significantly enhances the performance, SEO, and user experience of your application. By pre-rendering the application on the server and sending the fully rendered HTML to the client, users experience faster initial load times and improved interactivity.