
# Text Editor
Jate is a web application that provides a simple text editor with features like saving user input to IndexedDB database for offline use and using Workbox to register a service worker and pre-cache static assets. Jate is built using webpack and can be deployed to Heroku.

## Installation
To install and run Jate on your local machine, follow these steps:

Clone the repository to your local machine.
Run npm install to install the required dependencies.
Run npm run start to start the backend and serve the client.
Run the text editor application from your terminal.
Enter content and click off the DOM window to save the content to IndexedDB.
Close and reopen the text editor to retrieve the saved content from IndexedDB.
Usage
To use Jate, open the text editor and start typing. The application will automatically save your input to IndexedDB. To retrieve your saved content, simply reopen the text editor.

Built With
Jate is built using the following technologies:

IndexedDB API
Workbox
webpack

Code
The app.js file contains the main functionality of the application, using the CodeMirror library for text editing. The database.js file contains methods to save and get data from the IndexedDB database. When the editor is ready, the value is set to whatever is stored in IndexedDB. If nothing is stored in IndexedDB, it falls back to localStorage, and if neither is available, it sets the value to the header. The content of the editor is saved to IndexedDB when the editor loses focus.

In addition, Jate provides a client-server folder structure, starts the backend and serves the client when the command npm run start is run from the root directory, and bundles JavaScript files using webpack. It generates an HTML file, service worker, and manifest file using webpack plugins and provides a desktop icon when the Install button is clicked. A service worker is registered using Workbox, pre-caching static assets and subsequent pages and static assets. When the application is deployed to Heroku, proper build scripts are used for a webpack application.
