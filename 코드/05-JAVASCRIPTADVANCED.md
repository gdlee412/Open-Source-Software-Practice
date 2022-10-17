# Javascript Advamced

## Modules
open source packages for easier coding
https://www.npmjs.com/

## Node Package Manager (NPM)
Comes wth node and it is the package manager for Javascript / Node
needed for
    - dependency control
        - packages sometimes depend on other packages called dependencies
        - NPM will install all these dependensies
    - package update
        - packages usually get updated and they require new dependencies
        - to update the package, NPM will update all dependencies as well as the package
    - compatibility
        - different packages require different versions for dependencies
        - NPM will resolve these compatibility issues
    - prerequisite management
        - rather than including all of the used packages in a project, the NPM tracks the prerequisites of a project and carries this information with your project / package
        - just need the names and versions of packages
npm -v: check npm version
npm --help: see all commands

## Semantic Versioning
format for naming versions
version 1.2.3
1) Major version: major changes -> breaks the API
2) Minor version: minor changes -> does not break the API
3) Patches: bug fixes

safe to update packages with minor version or patch changes due to bug fixes and new / updated features

NOT safe to update major version changes due to compatibility -> must modify code to use this version

## package.json
every node contains this file in its root directory

it contains:
 - package name and versionf
 - description
 - keywords
 - homepage
 - license
 - dependencies
 - script

 ## Creating a Node Project
 type <npm init> in the root directory
    it will ask questions about your project
    press Enter to use default
    it will create package.json

## Install a Package
npm install <package name> - adds package to package.json as a dependency
        - creates a directory named node_modules under the root directory
        - download the source code of <package name> and save it to node_modules

example:
npm install hangul-js

dependencies installed via npm install are stored in node_modules
** Must add this directory to .gitignore **
otherwise the source code of all the dependencies will be under version control

use npm install and npm uninstall to add or remove a directory -> do not do it manually

### Three Installation Types
Local installation (npm install <name>)
    - dependencies used to run your package
    - <name> will be listed in dependencies in package.json
    - used when not sure which installation to use
Local dev installation (npm install <name> --save-dev)
    - for dependencies that are used to develop your package
    - <name> will be listed as dev-dependencies in package.json
    - packages for testing, linting, packaging, ...
Global installation (npm install -g <name>)
    - will not install <name> under node_modules but under a system-wide directory
    - <name> will NOT be listed in package.json
    - use command only when you install a command-line tool written in Javascript
    - in most cases, you will only install packages locally

## Use a Package
after installing, you can load a package into your Code
use <require>
intelliCode will help you see what's inside the package

example:
const hangul = require("hangul-js"); 

## Modules
create modules of your own

exports.<function>: can use this function / object in another project when this file is called 
<./filename>:  a local file in the same directory

example:
**circle.js**
const PI = Math.PI; 

exports.area = (r) => PI * r ** 2;
exports.circumference = (r) => 2 * PI * r;


**main.js**
const hangul = require("hangul-js"); 

console.log(hangul.disassemble("가나다"));
// <./circle.js> can be used since circle.js is in the same directory as main.js
const circle = require("./circle.js");

console.log('The are of a circle of radius 4 is ${circle.area(4)}');

# Case Study
Scenario: want to check the menu of the Cafeteria at Bldg. 26

Think of how we do it manually:

Today's date, 2022 10 3 webpage = 
https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&srDt=2022-10-03&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L

srDt shows the menu for a specific date
delete it and it will show today's menu

today's menu: https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L

## HyperText Markup Language (HTML)
HTML is a language that describes a web page given the code / text

Prepend "view-source:" to a url in Chrome to see the HTML code 

look for the menu in the HTML text:
view-source:https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L

once you find the menu names, use console.log to print the menu names

usually, doing this ("scrap from web pages") is illegal and needs permission

this is only an example for educational purposes
running this code too much will overload the server

## Download HTML from a url

googled "node https request"
  there was a link that used only Node.js standard modules
    always a good practice to use "standard modules" that comes with Node.js
    https://blog.bearer.sh/node-http-request/

    example code:
        const http = require("http");

        http.get("https://postman-echo.com/status/200",res -> {
            let data = ""

            res.on("data", d => {
                data += d
            })
            res.on("end", () => {
                console.log(data)
            })
        })

applying example code

const http = require("http");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

http.get(url, (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        console.log(data)
    });
});

node main.js
but there was an error:
https not supported

so changed http to https


const https = require("https");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

https.get(url, (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        console.log(data)
    });
});

node main.js
HTML document was received, but content was wrong

SKKU server considered my request unauthorized

when browser connects to a server, it sends extra information to the server in addition to the url you requested

HTTP headers
Referrrer: address of the previous web page from which a link to the currently requested page was followed
User-Agent: a characteristic string about your OS and web browser

However, if you connect to the page using the HTTPS module, these headers are not sent. So, from the server's point of view, your request seems unnatural


Let's add User-Agent

const https = require("https");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

https.get(url, {
    headers: {
        "User-Agent":  <user-agent>
    },
 },
 (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        console.log(data)
    });
});

this will finally give out the source code

## Parse HTML
html document consists of tags,
tags: strings contained in angle brackets
opening tag <html> vs closing tag </html>

tags constitute a hierarchy (a tree) called a DOM tree
DOM : document object model

Finding menu names = finding tags that contain menu names in the DOM three

but the downloaded HTML is just text, we must reconstruct the DO tree from HTML

HTML Parser constructs a DOM tree from an HTML document 

googled "node html parser"

seemed to be well maintained with many users and supporting the needed parse features


npm install node-html-parser

const https = require("https");
const parser = require("node-html-parser");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

https.get(url, {
    headers: {
        "User-Agent":  "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36"
    },
 },
 (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        let root = parser.parse(data);
    });
});

menu names are in a <div> tag that has a class atrribute "menu_title"

so we will find tags by class names

root.querySelectorAll(".menu_title") finds all tags who have a class name "menu_title" and returns an array of tags a '.' before the "menu_title" indicates that it is a class name

and then use the forEach method to print out the texts of menu names inside the tag

.trime() is called to remove leading and trailing whitespaces

" abc ".trim() => "abc"

const https = require("https");
const parser = require("node-html-parser");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

https.get(url, {
    headers: {
        "User-Agent":  "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36",
    },
 },
 (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        let root = parser.parse(data);
        root.querySelectorAll(".menu_title").forEach((menu) => {
            console.log(menu.innerText.trim());
        })
    });
});

this becomes the final code

we can only run this script inside the project directory for now

but we can install our package globally


## Develop a Command-line interface
1. Add "#!/ust/bin/env node" on the first line of main.js

#!/ust/bin/env node
const https = require("https");
const parser = require("node-html-parser");

let url = "https://www.skku.edu/skku/campus/support/welfare_11_1.do?mode=info&conspaceCd=20201104&srResId=3&srShowTime=D&srCategory=L";

https.get(url, {
    headers: {
        "User-Agent":  "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36",
    },
 },
 (res) => {
    let data = "";

    res.on("data", (d) => {
        data += d;
    });
    res.on("end", () => {
        let root = parser.parse(data);
        root.querySelectorAll(".menu_title").forEach((menu) => {
            console.log(menu.innerText.trim());
        })
    });
});


2. modify package.json as follows:

    "test": "echo\......
},
"bin": {
    "menu": "./main.js"
}
"author": "";
...

This bin property means that when this package is installed, you will expose a terminal command "menu" which runs "main.js"

3. npm pack
    will pack your code to a self-contained package

    example of the package
    npm notice name:    skku-menu
    npm notice version: 1.0.0
    npm filename:       skku-menu-1.0.0.tgz
    ...

4. npm install skku-menu-1.0.0.tgz -g
    install your package globally

5. menu
    you can now use the previous file globally by using "menu"

# Summary: Javascript Advanced
1. You can reuse Javascript packages to speed up your development
    - Dont reinvent the wheel
2. Using external packages introduces a lot of versioning and dependency issues, but a package manager will resolve them
    - Node Package Manager or NPM
3. package.json contains the metadata of your project. You must include this file in your project
4. We first developed a small but useful command line tool using Javascript