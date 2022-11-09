## If you Open SKKU-Todo
- You launch Chrome. The OS spawns a process.argv
- Type "```<link to ur skku todo>```"

- example of the Client Server Model
    - address: https://e-.github.io/skku-todo/index.html
    - Domain: e-github.io  -> translated to ip address
    - Your machine (no domain name)
        - ip = 132.234.12.4
    - Github's server ip = 185.199.108.153
```
    1. Query: file path: skku-todo/index.html
        - please give me index.html located in the skku-todo directory
        - NOT A PHYSICAL PATH
        - A request
    2. Github Server does a "Server Process" on this Request
    3. Github gives a response with the requested information
    4. We see the rendered result
```

# The Client-Server Model
- Client
    - Users
    - Make a request
    - Want to get some information or want something useful to happen
    - Your laptop, smartphone, ...
- Server
    - Given a request, make a response.
    - Have resources that a client want to retrieve
    - Always power on
    - Big computers in a dedicated server room
- Not physically separated. A web server process is a server for your browser but a client from DB's point of view

## Protocol
- A client and a server wants to communicate with each other
- They need to speak the same language
- **Protocol**: the official procedure or system of rules governing affairs of state or diplomatic occasions.
    - HTTP (HyperText Transfer Protocol)
    - HTTPS (HyperText Transfer Protocol Secure)
    - FTP, SSH, POP2, SMTP, ...

## HyperText Transfer Protocol
- A protocol for fetching resources such as HTML documents
- A request:
    - Method: GET, POST, OPTIONS, HEAD, ...
    - Path: the location of the resource
    - Headers: optional to convey additional information for the servers, e.g., browser information, ...
- A response:
    - Status Code: was the request successful?
    - Status Message: simple text description of the code
    - Headers
    - The body: the actual content of the fetched resource

## Method of a Request
- **GET**: simply retrieve a resource without changing it.
- **POST**: submit an entity to the server, hoping for changes.
    - Sign up forms: username/password are transferred
    - Your state should change to "logged in"
    - Not safe (it changes the erver state) nor idempotent (multiple identical requests will not have the same outcome)
- **HEAD**: Same as GET without the body
- PUT, DELETE, OPTIONS, ...

## Status Code of a Response
HTTP Status codes
- 2xx Success
    - 200: Success / OK
- 3xx Redirection
    - 301: Permanent redirect
    - 302: Temporary redirect
    - 304: Not Modified
- 4xx Client Error
    - 401: Unauthorized Error
    - 402: Forbidden
    - 404: Not Found
    - 405: Method Not Allowed
- 5xx Server Error
    - 501: Not implemented
    - 502: Bad Gateway
    - 503: Service Unavailable
    - 504: Gateway Timeout

## HTTP
- Use the inspector tool to see the actual request and response

## Port
- Sometimes, there's a number in the url after the domain
    - http://www.my-domain.com:8080/page/I/want/to/see
- Port of the host that I want to connect (Optional)
- A host computer can have multiple server processes at the same time.
    1. Process 1: HTTP,  listening to 80 (default)
    2. Process 2: HTTPS, listening to 443 (default)
    3. Process 3: RDP, listening to 3389 (default)
    4. Changes Process 3: to HTTP, listening to 8080

## Let's Make a Server
- Frameworks for the server-side development:
    - Express.js(JS)
    - Django (Python)
    - Flask (Python)
    - Spring (Java)
    - Ruby on Rails (Ruby)
    - PHP
    - ...

## Express.js
- **Express.js**: a very minimal yet powerful web framework for node.js
- npm install express
    - We will use 4.x.
- Let's write a "Hello, World!" server.
- https://github.com/e-/skku-chat

## Hello, World!
- Type the following code in main.js.
- node main.js
    - **CTRL + C** to exit
```js
const express = require('express')  //import express.js

//create a new app
const app = express()
const port = 3000

//an event-listener-like specification
//if you get a GET request on "/", send "Hello, World" to the client
app.get('/', (req, res) => {
    res.send('Hello, World!')
})

//Run the app on port 3000
//The process will go into an infinite loop until Ctrl + C
app.listen(port, () => {
    console.log('Example app listening on port ${port}')
})
```
- navigate to http://localhost:3000 or http://127.0.0.1:3000
- 127.0.0.1 = a computer locating / pointing at itself (not universal)

## Serving a File
- We could send a text message to the client as a response
- What about sending an HTML code?

- Create a directory "public"
    - The files under this directory will be directly served to clients
    - Don't put any private files., e.g., main.js (source code of the server itself)

- Create index.html under public, and type the code on the next page.

## Client Code
```html
<!DOCTYPE html>
<html>
    <head>
        <title>SKKU-CHAT</title>
        <link rel="stylesheet" href = "https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/css/bootstrap.min.css" integrity = "sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    </head>
    <body>
        <div class="container">
            <p>
                Visits so far: <span id="counter"></span>
            </p>
        </div>
        <script>
        </script>
    </body>
</html>
```

## Server Code
```js
const express = require('express')  //import express.js

//create a new app
const app = express()
const port = 3000

//an event-listener-like specification
//if you get a GET request on "/", send "Hello, World" to the client
//app.get('/', (req, res) => {
//    res.send('Hello, World!')
//})

app.use(express.static('public'))

//Run the app on port 3000
//The process will go into an infinite loop until Ctrl + C
app.listen(port, () => {
    console.log('Example app listening on port ${port}')
})
```

## Counting the Visits
- Let's make something useful: visit counter.
- Once the page is loaded, send a request to the server **again** (without a refresh!) to load the # of visitors.
- You can issue a request using JS without refreshing the page.
- Long ago, this was new and specially called AJAX (Asynchronous JavaScript and XML)
- But these days, we don't consider it special since everyone uses it. It became de facto standard of the Web.

## The fetch() API
- How can we make a request using JS? Use the fetch() API
- Example: fetch (url, options).then(handler)

```js
fetch(
    "localhost:3000/counter",
    {method: "GET"})
    .then((count) => { })
```

## Client Code
```html
<!DOCTYPE html>
<html>
    <head>
        <title>SKKU-CHAT</title>
        <link rel="stylesheet" href = "https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/css/bootstrap.min.css" integrity = "sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    </head>
    <body>
        <div class="container">
            <p>
                Visits so far: <span id="counter"></span>
            </p>
        </div>
        <script>
            //when the page is loaded
            window.addEventListener("load", () => {
                fetch("/counter", { method: "GET" })    //fetch the "/counter" resource
                    .then((res) => res.text())  //get the result as text
                    .then((count) => {
                        let counter = document.getElementById("counter");
                        counter.textContent = count;   
                    })  //and put the text into the #counter element
            })
        </script>
    </body>
</html>
```

## Server Code
```js
const express = require('express')  //import express.js

//create a new app
const app = express()
const port = 3000

app.get('/counter', (req, res) => { //When someone requests "/counter"
    counter++;  //increment the global counter variable
    res.send(counter.toString())    //and return the counter as text
})

app.use(express.static('public'))

//Run the app on port 3000
//The process will go into an infinite loop until Ctrl + C
app.listen(port, () => {
    console.log('Example app listening on port ${port}')
})
```

## Simple Chat App
- In the previous example, we just requested a resource to the server without attaching extra data.
- Can we send data to the server?
- Let's make a very simple chat app.

## Client Code - HTML
```html
<h2>Chat</h2>
<ul id="chats">

</ul>
<div class="d-flex">
    <input type="text" id="chat" class="form-control" placeholder="Enter a chat here">
    <button type="submit" id="submit" class="btn btn-primary">Submit</button>
</div>
```

## Client Code - JS
- Getting the messages from the server.
- Clear the list and append the <li> elements for the messages.

```js
function loadChats() {
    fetch("/chats", {method: "GET"})
        .then((res) => res.json())
        .then((chats) => {
            let list = document.getElementById("chats");
            list.innerHTML = "";

            chats.forEach(chat => {
                let li = document.createElement("li");
                li.textContent = chat;
                list.appendChild(li);
            })
        })
}
```
- When the user clicks on the submit button, read the text in the ```<input>``` tag and send it to the server as a JSON object.

```js
document.getElementById("submit").addEventListener("click", () => {
    let input = document.getElementById("chat");
    let chat = input.value;

    fetch("/chats", {
        method: "POST",
        headers: {
            'Content-Type' : 'application/json',
        },
        body: JSON.stringify({ chat })
    })
        .then(() => {
            loadChats();
        })
})
```

## Simple Chat Server
```js
const express = require('express')
const app = express()
const port = 3000

app.get('/counter', (req, res) => {
    counter++;
    res.send(counter.toString())
})

app.use(express.json()) // for parsing application / json

let chats = [];

app.get('/chats', (req, res) => {
    res.send(chats);
})

app.post('/chats', (req, res) => {
    chats.push(req.body.chat);
    res.send(200);
})

app.use(express.static('public'))

app.listen(port, () => {
    console.log('Example app listening on port ${port}')
})
```

## Server Push
- Open "localhost:3000" on Tab 1
- Submit a chat message "Hello"
- Open "localhost:3000" again on Tab 2
- The message should be visible on Tab 2

- If we enter message in Tab 1, is Tab 2 updated? No.
- Tab 2 does not know whether there is a new message on the server.

## Limitation of HTTP 1.1: 
- The client only initiates a request
- There is no way for the server to notify the client of something
    - e.g., chat application
- However, there ARE chat applications on the Web. How do they work?
- They are using the "server-push" technologies, e.g., WebSocket.
- But, we are not going further about this
- Anyway, "real-time" Web applications are everywhere these days

## Server Push (continued)
- One workaround to this problem is to use "polling"
- Load the messages from the server every one second.
- Simple but inefficient if there is no update.
```js
setInterval(loadChats, 1000); //implements polling
```

## SKKU-Chat
- If you exit a server process, all messages are gone. You need to store the messages if you want them to be persistent. Use a database.
- Others cannot connect your server if your IP is not public. If you want to host a server, you need to have a public and static IP address.
- You cannot fetch pages under a different domain (e.g., accessing google.com:80 from localhost:3000).
- The chat app we developed is unsafe. Never use it in the real world.
- GitHub Pages will not work for SKKU-Chat since it simply delivers the files statistically without actually executing the main.js script.

## Python Open Source?
- Different programming languages have different ecosystems.
- However, they share important concepts!
    - A package manager, package index, metadata files...

<table>
    <tr>
        <th></th>
        <th>JavaScript (on Node.js)</th>
        <th>Python</th>
    </tr>
    <tr>
        <td>Command</td>
        <td>node</td>
        <td>python / python 3</td>
    </tr>
    <tr>
        <td>Package Index</td>
        <td>NPM</td>
        <td>PyPI</td>
    </tr>
    <tr>
        <td>Package manager command</td>
        <td>npm</td>
        <td>pip</td>
    </tr>
    <tr>
        <td>Metadata</td>
        <td>package.json</td>
        <td>setup.py</td>
    </tr>
    <tr>
        <td>Publish</td>
        <td>npm publish</td>
        <td>twine upload</td>
    </tr>
</table>

# Summary: OSSP
- Git and GitHub
- VSCode, Plugins, editoryconfig, ...
- Node, JavaScript, HTML, and CSS
- Unit Testing
- Automation using GitHub Actions
- Publishing using GitHub Pages
- Cross-platform apps using Electron
- Collaboration (pull requests, issues, ...)
- Client-server model
- a command line app, a Web app, a desktop app, a Web page, and a simple chat app that uses the client-server architecture