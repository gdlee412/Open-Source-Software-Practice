# Web Application

## HTMLANDCSS (continued)
Front-end Toolkits: reusable CSS and JS code for web development
Bootstrap: one of the most popular front-end toolkits (open source)
https://getbootstrap.com/
v5.2.2
Originally developed by Twitter

CSS components: layout, form, button, list, navigation, ...
JS components: dialog, toast message, accordion, ...

# SKKU-Todo
Creating a Web application SKKU-Todo: a simple task management app
All the templates will be based from bootstrap

Features:
- Add tasks
- Remove tasks
- Mark as done
- Save and restore

## Adding a container
define a global container: all components resided in this container
create <div> with class name "container"
default width of container = 1320px -> defined by Bootstrap

<div class="container">
    This is the container!
</div>

## Adding a Navbar
Let's create a simple navigation bar
<nav class = "navbar navbar-light bg-light">
    <div class="container">
        <span class = "navbar-brand mb-0 h1">SKKU-Todo</span>
    </div>
</nav>
<div class="container">
    This is the container!
</div>

## Adding a Form
Create a form where the user can enter a task name
- text box + button

Find an example suitable for us:
change the text inside <label> to "Task"
change the input type from "email" to "text" to receive any text
change the placeholder to "enter a task"

<nav class = "navbar navbar-light bg-light">
    <div class="container">
        <span class = "navbar-brand mb-0 h1">SKKU-Todo</span>
    </div>
</nav>
<div class="container">
    <div class = "mb-3">
        <label for="exampleFormControlInput1" class ="form-label">Task</label>
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
    </div>
</div>

## Adjusting the Width
Let's adjust the width of container class by adding a CSS Rule

<style>
    .container {
        width: 640px;
    }
</style>

## Adding a Button
Button with class "btn-primary"
Place button in <div> just below <input>

<div class="container">
    <div class = "mb-3">
        <label for="exampleFormControlInput1" class ="form-label">Task</label>
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
        <button type="button" class="btn btn-primary">Add</button>
    </div>
</div>

## Adding Lists
We need two lists, one for todos and other for completed tasks
We will use the following markup:

<div class="container">
    <div class = "mb-3">
        <label for="exampleFormControlInput1" class ="form-label">Task</label>
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
        <button type="button" class="btn btn-primary">Add</button>
    </div>
    <div>
        <div>
            <h3>Todos</h3>
            <div id="todo-list">
                <div class="task">Sample task</div>
            </div>
        </div>
        <div>
            <h3>Done</h3>
            <div id="done-list">
            </div>
        </div>
    </div>
</div>

## Styling the Interface
Let's improve the interface

1. Side-by-Side layout
2. Adjusting the space around components
3. Using Icons

by default, HTML block elements are stacked vertically
Put them in flexbox for side-by-side placement
examples in bootstrap:
1. https://getbootstrap.com/docs/5.2/utilities/flex/
2. https://css-tricks.com/snippets/css/a-guide-to-flexbox/

children under <div> with "d-flex" class will be placed side-by-side ("d" means "display")
components in first flexbox should be vertically aligned to center:
    - Add "align-items-center" class to the first flexbox
the two lists should occupy the same width: 
    - Add "flex-grow-1" class to the wrapper of the two lists

<div class="container">
    <div class = "d-flex align-items-center mb-3">
        <label for="exampleFormControlInput1" class ="form-label">Task</label>
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
        <button type="button" class="btn btn-primary">Add</button>
    </div>
    <div class = "d-flex">
        <div class="flex-grow-1">
            <h3>Todos</h3>
            <div id="todo-list">
                <div class="task">Sample task</div>
            </div>
        </div>
     <div class="flex-grow-1">
            <h3>Done</h3>
            <div id="done-list">
            </div>
        </div>
    </div>
</div>

Let's now adjust the space between components by adjusting padding and margins

Bootstrap provides utility classes which are useful to control appearances of tags without adding CSS rules
- Background colors
- Borders
- Colors
- Padding and margins
- Shadow
- Text

For padding and margins
{property}{sides}-{size}
property: m(margin), p(padding)
sides: t(top), b(bottom), s(start / left), e(end / right), x(left and right), y(top and bottom)
size: integers from 0 to 5 where 1 = 0.25rem

Examples:
"ms-1": left margin to 0.25rem
"px-2": left and right paddings to 0.5rem
"ms-1 ps-1": left margin and padding to 0.25rem
"m-1": all side margins to 0.25rem
"m-0 p-0" remove all paddings and margins

"w-50": width:50&
<label> removed for Simplicity

<div class="container">
    <div class = "d-flex align-items-center mb-2 mt-2">
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
        <button type="button" class="btn btn-primary">Add</button>
    </div>
    <div class = "d-flex">
        <div class="flex-grow-1 bg-light rounded-2 p-2 me-1 w-50">
            <h3>Todos</h3>
            <div id="todo-list">
                <div class="task bg-light p-1 rounded-2 ps-2">Sample task</div>
            </div>
        </div>
     <div class="flex-grow-1 bg-light rounded-2 p-2 w-50">
            <h3>Done</h3>
            <div id="done-list">
            </div>
        </div>
    </div>
</div>

Finishing touch by adding icons
Bootstrap provides an icon extension
https://icons.getbootstrap.com/
<i class="bi-alarm"></i>

<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap...">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.4.1/font/bootstrap-icons.css">



<nav class = "navbar navbar-light bg-light">
    <div class="container">
        <span class = "navbar-brand mb-0 h1"><i class="bi bi-card-checklist"></i>SKKU-Todo</span>
    </div>
</nav>
<div class="container">
    <div class = "d-flex align-items-center mb-2 mt-2">
        <input type = "text" class = "form-control" id="exampleFormControlInput1" placeholder="Enter a task here"> 
        <!--if image breaks, add "text-nowrap"-->
        <button type="button" class="btn btn-primary"><i class="bi bi-plus"></i>Add</button>
    </div>


## Adding interactions
let's make out program interactive
When user clicks the "Add" button, the text in text box will be appended to the "Todos" list
we will do this using Javascript
    When "Add" button is clicked,
    Read task name in textbox
    Append the name to the list
    clear textbox


Some id setups before interactions

<div class="container">
    <div class = "d-flex align-items-center mb-2 mt-2">
        <input type = "text" class = "form-control" id="task-input" placeholder="Enter a task here"> 
        <!--if image breaks, add "text-nowrap"-->
        <button type="button" id="add" class="btn btn-primary"><i class="bi bi-plus"></i>Add</button>
    </div>
    <div class = "d-flex">
        <div class="flex-grow-1 bg-light rounded-2 p-2 me-1 w-50">
            <h3>Todos</h3>
            <div id="todo-list">
                <div class="task bg-light p-1 rounded-2 ps-2">Sample task</div>
            </div>
        </div>
     <div class="flex-grow-1 bg-light rounded-2 p-2 w-50">
            <h3>Done</h3>
            <div id="done-list">
            </div>
        </div>
    </div>
</div>

if #add is clicked,
read #task-input
append to #todo-list
clear #task-input type

### Event Handling
for button clicks, page loading, etc., we attach an event handler to the HTML element (#add in our case)
Event handler: function that is called whenever corresponding event occurs

select element to which the event handler is attached
document.querySelector("#add") returns an HTML element whose id is "add"

(element).addEventListener(type, listener) adds a function listener that will be called when the specified event occurs
    types: "click", "dblclick", "mouseenter", "mouseleave", "keydown",...
    https://developer.mozilla.org/en-US/docs/Web/Events

let button = document.querySelector("#add");

button.addEventListener("click", () => {
    console.log('Clicked!');
    // 1. Read text in "#task-input"
    // 2. Append the text to #todo-list
    // 3. Clear #task-input
})

### Getting input
To get a text in an input box, first select the input box
    document.querySelector("#task-input")
    (element).value contains value of elemet

let button = document.querySelector("#add");

button.addEventListener("click", () => {
    // 1. Read text in "#task-input"
    let input = document.querySelector("#task-input");
    let task = input.value;
    console.log(task);

    // 2. Append the text to #todo-list
    // 3. Clear #task-input
})

### Creating an Element
document.createElement(tagName) creates a new tag in memor
you must append the created tag to an element that is on screen to make it visible
dont forget to add classes for styling

let button = document.querySelector("#add");

button.addEventListener("click", () => {
    // 1. Read text in "#task-input"
    let input = document.querySelector("#task-input");
    let task = input.value;

    // 2. Append the text to #todo-list
    let newTask = document.createElement("div");
    newTask.classList.add("task", "bg-light", "p-1", "rounded-2", "ps-2");
    newTask.textContent = task;

    let todoList=document.querySelector("#todo-list");
    todoList.appendChild(newTask);

    // 3. Clear #task-input
})

<div id= "todo-list">
    <div class="task bg-light p-1 rounded-2 ps-2">Sample task</div>
</div>

### Clearing the Input
Finally, clear the input once a task is added

let button = document.querySelector("#add");

button.addEventListener("click", () => {
    // 1. Read text in "#task-input"
    let input = document.querySelector("#task-input");
    let task = input.value;

    // 2. Append the text to #todo-list
    let newTask = document.createElement("div");
    newTask.classList.add("task", "bg-light", "p-1", "rounded-2", "ps-2");
    newTask.textContent = task;

    let todoList=document.querySelector("#todo-list");
    todoList.appendChild(newTask);

    // 3. Clear #task-input
    input.value = "";
})

add an if statement to prevent empty tasks from being added

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

## Let's Publish
Congrats! We just developed a Web app
Let's publish it to the Web using GitHUb's free Web hosting service

1. Create a Github repository, the name will be part of url
2. Make sure the name of the HTML file is "index.html": means the landing page
3. Commit the HTML file to the repository
4. In Github repository, go to Settings -> Pages. Set the Source to "Branch:main" and Save

Web demo: https://e-github.io/skku-todo/
Github repository: https://github.com/e-/skku-todo

# Summary
In this class, we developed a simple Web app for task management
    - We will extend its features next time
Bootstrap is a collection of CSS styles (+JS code) that can accelerate web development
    - Container, navbar, button, forms, and many utility classes!
JavaScript brings interactivity to your app
    - There are special function that bridge HTML and JS such as document.querySelector
    - (element).addEventListener(name, handler) sets up a function that is called each time a specific event happens
    - Accessing the value of <input> tags via the value attributes