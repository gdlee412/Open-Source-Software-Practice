# Desktop App

## SKKU Todo
Let's improve SKKU-Todo
- Remove a task
- Save and restore
- Mark as done

Skeleton code
<!DOCTYPE html>
<html lang="en">
    <head>
        <!--Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        
        <!--Bootstrap CSS-->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet" crossorigin="anonymous">
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.4.1/font/bootstrap-icons.css">
        <title>GwunLe's Beautiful Todo List</title>
        <style>
            .container {
                width: 640px;
            }
        </style>
    </head>
    <body>
        <nav class="navbar navbar-light bg-light">
            <div class="container">
                <span class="navbar-brand mb-0 h1"><i class="bi bi-card-checklist"></i>SKKU-Todo</span>
            </div>
        </nav>
        <div class="container">
            <div class="d-flex align-items-center mb-2 mt-2">
                <input type="text" class="form-control" id="task-input" placeholder="Enter a task here">
                <button type="button" id="add" class="btn btn-primary ms-1 text-nowrap"><i class="bi bi-plus"></i>Add</button>
            </div>
        </div>

        <div class = "d-flex">
            <div class="flex-grow-1 bg-light rounded-2 p-2 me-1 w-50">
                <h3>Todos</h3>
                <div id="todo-list">
                    <div class="task bg-light p-1 rounded-2 ps-2"></div>
                </div>
            </div>
         <div class="flex-grow-1 bg-light rounded-2 p-2 w-50">
                <h3>Done</h3>
                <div id="done-list">
                </div>
            </div>
        </div>

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js" crossorigin="anonymous"></script>
        <script>
            let button = document.querySelector("#add");

            button.addEventListener("click", () => {
                // 1. Read text in "#task-input"
                let input = document.querySelector("#task-input");
                let task = input.value;

                if(!task.length) return;

                // 2. Append the text to #todo-list
                let newTask = document.createElement("div");
                newTask.classList.add("task", "bg-light", "p-1", "rounded-2", "ps-2");
                newTask.textContent = task;

                let todoList=document.querySelector("#todo-list");
                todoList.appendChild(newTask);

                // 3. Clear #task-input
                input.value = "";
            })
        </script>
    
    </body>
</html>

## HTML
We need two buttons for each task item

<div id="todo-list">
    <div class="task bg-light p-1 rounded-2 ps-2 d-flex aligh-items-center">
        <span class="me-auto">Task text</span>
        <button class="btn btn-sm btn-success me-1">
            <i class="bi bi-check"></i>
        </button>
        <button class="btn btn-sm btn-DANGER">
            <i class="bi bi-x"></i>
        </button>
    </div>
</div>

## Adding a Task
we will manage a task as an object with the following properties:
1. text: string, the task name
2. type: number, the task type (1 for todo and 2 for done)

const Type = {
    Todo: 1,
    Done: 2,
}

let button = document.querySelector("#add");

button.addEventListener("click", () => {
    // 1. Read text in "#task-input"
    let input = document.querySelector("#task-input");
    let task = input.value;

    if(!task.length) return;

    // 2. Create a new Task object
    let task = {
        text: text,
        type: Type.Todo
    }

    // 3. Create a new task item and attack it to #todo-lists
    addToList(task);

    // 3. Clear #task-input
    input.value = "";
})

Function addToList receives a task object and creates a list object
Depending on task.type, item will append to either #todo-list or #done-list

To add to list, we must generate an HTML code

Our weapons:
    document.createELement(name)
    element.appendChild(child)
    element.className = "abc"
    element.innerHTML = "<i></i>"

function addToList(task) {
    let div = document.createElement("div");
    div.className = "task bg-light p-1 rounded-2 ps-2 d-flex align-items-center";

    //append span to div
    let span = document.createElement("span");
    span.className = "me-auto";
    span.textContent = task.text;
    div.appendChild(span);

    // add the check button
    if(task.type === Type.Todo) {
        let buttonDone = document.createElement("button");
        buttonDone.className = "btn btn-sm btn-success me-1";
        buttonDone.innerHTML = "<i class = "bi bi-check"></i>";
        div.appendChild(buttonDone);
    }

    //add the remove button
    let buttonRemove = document.createElement("button");
    buttonRemove.className = "btn btn-sm btn-danger";
    buttonRemove.innerHTML = "<i class = "bi bi-class"></i>";
    div.appendChild(buttonRemove);

    //depending on type, append to todo or done list
    let list = document.querySelector(task.type === Type.Todo ? "#todo-list" : "#done-list");
    list.appendChild(div);
}

## Removing a Tasks
Now add the functionality of the remove button
remove the div if clicked


let buttonRemove = document.createElement("button");
buttonRemove.className = "btn btn-sm btn-danger";
buttonRemove.innerHTML = "<i class = "bi bi-class"></i>";
div.appendChild(buttonRemove);

buttonRemove.addEventListener("click", () => {
    div.remove();
});

//depending on type, append to todo or done list
let list = document.querySelector(task.type === Type.Todo ? "#todo-list" : "#done-list");
list.appendChild(div);

The variable div was not defined in the function addEventListener, but inner functions have access to the variables of outer function
div was included in the environment of the function

## Saving and lOading the State
Our app is currently volatile, disappearing after every refresh
Let's save the tasks using localStorage: data persists even if you exit the browser

localStorage.setItem(key, value): associates a string value to key
localStorage.getItem(key) returns the value associated with key

### 1. Defining the States
When implementing saving/loading, consider the following:
1. What is the "state" of a program?
2. How do user interactions change the state?
3. How to save the state?
4. How to load the state and initialize interfaces from it?

SKKU-Todo can be defined as an array of tasks

We can maintain this state using a global array, tasks

let tasks = [];

### 2. Changing the State
(addition): when new task is added, push the task object to tasks
(deletion): when task is removed, filter out the task object from tasks

ADDITION:
// 2. Create a new task object
let task = {
    text: text,
    type: Type.Todo
};

//3. Append the new Task objects to tasks
tasks.push(task);

DELETION:
buttonRemove.addEventListener("click", () => {
    div.remove();
    tasks = tasks.filter(t => t !== task);
})

### 3. Saving the State
Save the tasks array in the local storage
Since local storage can only store string values, convert the objects to string
JSON.stringify(obj) does this

function saveTasks(){
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

call save Tasks every time user changes the state

ADDITION:
// 2. Create a new task object
let task = {
    text: text,
    type: Type.Todo
};

//3. Append the new Task objects to tasks
tasks.push(task);
saveTasks();

DELETION:
buttonRemove.addEventListener("click", () => {
    div.remove();
    tasks = tasks.filter(t => t !== task);
    saveTasks();
})

### 4. Loading the State
When app is loaded, read the state string from local storage
set tasks
populate list items

when the app is loaded -> event handling
    - event fired by browser, not user

window.addEventListener("load", () => {
    loadTasks();
});

JSON.parse(string) converts string to object

function loadTasks(){
    let lastTasks = localStorage.getItem("tasks");
    if(!lastTasks) return;

    tasks = JSON.parse(lastTasks);
    tasks.forEach(addToList);
    /*
    tasks.forEach(t => {
        addToList(t);
    });
    */
}

## Let's Publish
Electron is a framework that builds cross-platform desktop apps using Web technologies
    Slogan: If you can build a website, you can build a desktop application
https://www.elecytonjs.org/
https://www.electronjs.org/docs/tutorial/quick-start

You need at least four files:
1. package.json: create using npm init
2. main.js: use default file from official documentation
            https://www.electronjs.org/docs/tutorial/quick-start
            https://github.com/e-/skku-todo-2/blob/main/main.js
3. preload.js: Create an empty JS file
4. index.html: HTML file

Main.js:

const{app, BrowserWindow} = require('electron')
const path = require('path')

function createWindow(){
    const win = new BrowserWindow({
        width: 800,
        height: 600,
        webPreferences: {
            preload: path.join(__dirname, 'preload.js')
        }
    })

    //remove menu bar
    win.setMenuBarVisibility(false);
    win.loadFile('index.html')
}

app.whenReady().then(() => {
    createWindow()

    app.on('activate', () => {
        if(BrowserWindow.getAllWindows().length === 0) {
            createWindow()
        }
    })
})

app.on('window-all-closed', () => {
    if(process.platform !== 'darwin') {
        app.quit()
    }
})


npm install --save-dev @electron-forge/cli
npx electron-forge import
//package.json will be converted

npm start
// SKKU-Todo became a desktop app!
// check if all features work as expected.

make package for distribution
npm run make
// No Korean in the pathway


find package in the "out" directory

zip and ship all files to distribute your app


## What's next?
We learned HTML, CSS, JS...
We learned Node.js, Bootstrap, and unit testing
We built and published a command-line interface(skku-menu), a Web app(skku-todo), and a desktop app (skku-todo-2)

To level up your dev skills further, learn:
1. JS components of Bootstrap, Twitters's toolkit to enrich your user interface
2. React, Facebook's JS library to build reactive apps
3. TypeScript, Microsoft's Typed JavaScript
4. Flutter, Google's UI toolkit for building cross platform apps

Mastering a few of these will make you survive