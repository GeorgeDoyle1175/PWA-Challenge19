# Text Editor

Jate is a web application that provides a simple text editor with features like saving user input to IndexedDB database for offline use and using Workbox to register a service worker and pre-cache static assets. Jate is built using webpack and can be deployed to Heroku.

This repository also contains a service worker file (`src-sw.js`) that defines caching strategies for different types of network requests to ensure optimal loading performance and offline functionality. The service worker file is configured to use Workbox, a set of libraries that implement best practices for service workers.

DEPLOYED APPLICATION Visit the website [here](https://challenge19miami.herokuapp.com/).

## Service Worker (`src-sw.js`)

The service worker file uses Workbox to precache files, implement cache-first strategies for page and asset requests, and set up cache expiration policies.

- `precacheAndRoute(self.__WB_MANIFEST)`: This line precaches files listed in the Webpack-generated manifest. This ensures that important files are available offline from the start.

- `CacheFirst` strategy is defined for pages (HTML requests) and assets (like images, CSS, and JavaScript files). This strategy attempts to respond with a cached response first, and falls back to the network if the cache does not contain the requested file.

- `CacheableResponsePlugin` is used with both strategies to ensure only responses with status 0 or 200 are cached.

- `ExpirationPlugin` is used with both strategies to remove outdated cache entries. For pages, the maximum age is set to 30 days and for assets, the maximum age is set to 7 days.

- The `warmStrategyCache` function call warms the page cache for the specified URLs ('/index.html' and '/').

- `registerRoute` method is used to apply the caching strategies to different types of requests. It is used to cache navigational requests using the page caching strategy and to cache assets using the assets caching strategy.

## Installation

To install and run Jate on your local machine, follow these steps:

1. Clone the repository to your local machine.
2. Run `npm install` to install the required dependencies.
3. Run `npm run start` to start the backend and serve the client.
4. Run the text editor application from your terminal.
5. Enter content and click off the DOM window to save the content to IndexedDB.
6. Close and reopen the text editor to retrieve the saved content from IndexedDB.

## Usage

To use Jate, open the text editor and start typing. The application will automatically save your input to IndexedDB. To retrieve your saved content, simply reopen the text editor.

## Built With

Jate is built using the following technologies:

- IndexedDB API
- Workbox
- webpack

## Code

The `app.js` file contains the main functionality of the application, using the CodeMirror library for text editing. The `database.js` file contains methods to save and get data from the IndexedDB database. When the editor is ready, the value is set to whatever is stored in IndexedDB. If nothing is stored in IndexedDB, it falls back to localStorage, and if neither is available, it sets the value to the header. The content of the editor is saved to IndexedDB when the editor loses focus.

The `webpack.config.js` file defines the configuration for the webpack bundler. It specifies the entry points for the application (`index.js` and `install.js`), the output directory (`dist`), and the filename pattern for the bundled assets. It also defines the plugins to be used during the build process:

- `HtmlWebpackPlugin`: Generates an HTML file for the application.
- `WebpackPwaManifest`: Generates a web app manifest for the PWA. It specifies metadata such as the name, short name, description, theme color, and icons for the app.
- `InjectManifest`: A Workbox plugin that generates a list of local files that should be cached by the service worker.

In addition, Jate provides a client-server folder structure, starts the backend, and serves the client when the command `npm run start` is run from the root directory. The JavaScript files are bundled using webpack. It generates an HTML file, service worker, and manifest file using webpack plugins and provides a desktop icon when the Install button is clicked. A service worker is registered using Workbox, pre-caching static assets and subsequent pages and static assets. When the application is deployed to Heroku, proper build scripts are used for a webpack application.
