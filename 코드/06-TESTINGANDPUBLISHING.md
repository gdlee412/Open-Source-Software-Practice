# Testing and Publishing


## Setup
1. Create a github repository
2. with gitignore file for Node
3. Clone repository
 - using git pull origin main --allow-unrelated-histories
4. Open project on VSCode and tyipe npm init in Terminal
 - Generate .editorconfig and use default settings
5. modify version to 0.1.0 from 1.0.0 in package.json

## Command-Line Arguments
1. command to run: stat sum 1 2 3
    result: 6

2. We need to read the command-line arguments after the command name
    they are stored in an array <process.argv>
    argv[0] = path to the Node runtime
    argv[1] = path to the current file
    argv[2] = operation type
    argv[3] = there are numbers as strings
        there are (process.argv.length - 3) numbers in total

3. array.slice(a, b) creates a new array using elements from a to b
        - array.slice(3, array.length) will select from index 3 to the end
    array.map(f) collects the return values of a function after applying it to each element
    parseFloat(n) converts a string to a number

    let command = process.argv[2]

    let numbers = process.argv.slice(3, array.length).map((n) => parseFloat(n));

4. switch - case statement to process the command types
    store results in the result variable, which will be logged at the end
    if command is not "sum", "avg", "max", print error
    - process.exit(1) exits the program with a return value 1 (error code)

    let command = process.argv[2]

    let numbers = process.argv.slice(3, array.length).map((n) => parseFloat(n));

    let result;
    switch(command){
        case "sum":
            break;
        case "avg":
            break;
        case "max":
            break;
        default:
            console.log("Wrong command!");
            process.exit(1);
    }

    console.log(result);

5. Separating the Logics
    write the functions for each case and try defining it into a different library lib.js

    function sum(numbers){
        let s = 0;
        for(let i = 0; i < numbers.length; i++){
            s+= numbers[i];
            return s;
        }
    }

    function avg(numbers){
        return sum(numbers) / numbers.length;
    }

    function max(numbers){
        let m = numbers[0];
        for(let i = 1; i < numbers.length; i++){ if (m < numbers[i]) m = numbers[i]
        return m;
        }
    }

    exports.sum = sum;
    exports.avg = avg;
    exports.max = max;

6. Making the codes more functional
    function sum(numbers){
        return numbers.reduce((prev, curr) => prev + curr, 0);
        //0 means the initial prev value
    }

    function avg(numbers){
        return sum(numbers) / numbers.length;
    }

    function max(numbers){
        return numbers.reduce((max, curr) = > (max > curr ? max : curr), numbers[0])
        //numbers[0] is the initial max value
    }

    module.exports = {
        sum,
        avg,
        max,
    }

7. main.js

load lib.js and use the functions

    const lib = require("./lib");

    let command = process.argv[2]

    let numbers = process.argv.slice(3, array.length).map((n) => parseFloat(n));

    let result;
    switch(command){
        case "sum":
            result = lib.sum(numbers);
            break;
        case "avg":
            result = lib.avg(numbers);
            break;
        case "max":
            result = lib.max(numbers);
            break;
        default:
            console.log("Wrong command!");
            process.exit(1);
    }

    console.log(result);

8. Error Handling

    1. command is not sum, avg, and max
        already handled
    2. insufficient number of parameters
        at least one command and one number
        if(process.argv.length <= 3){
            console.log("Insufficient parameter!");
            process.exit(1);
        }

    3. if parameter is not a number
        if(numbers.some((n) => isNaN(n)){
            console.log("Some arguments are not numbers!");
            process.exit(1);
        }
        parseFloat before this code returns NaN for not a number arguments

    have error code 1 for either of them

9. Linking a Command

    1. add #!/usr/bin/env node to the first line of main.js
    2. Link main.js to a command in package.json
    "bin": {
        "stat": "./main.js"
    }
    3. npm link
    4. you should be able to run the "stat" command
    5. Dont forget to run npm unlink <name> after testing commands


10. main.js

    #!/usr/bin/env node
    const lib = require("./lib");

    if(process.argv.length <= 3){
            console.log("Insufficient parameter!");
            process.exit(1);
        }

    let command = process.argv[2]

    let numbers = process.argv.slice(3, array.length).map((n) => parseFloat(n));

    if(numbers.some((n) => isNaN(n)){
            console.log("Some arguments are not numbers!");
            process.exit(1);
        }

    let result;
    switch(command){
        case "sum":
            result = lib.sum(numbers);
            break;
        case "avg":
            result = lib.avg(numbers);
            break;
        case "max":
            result = lib.max(numbers);
            break;
        default:
            console.log("Wrong command!");
            process.exit(1);
    }

    console.log(result);


## Testing
With the previous code, we manually tested the codes

But what if the program gets bigger?
 - more components
 - complex scenarios
 - heterogenous environments(e.g. Node.js versions)
 - different developers

we need to automate the test

### Unit testing
Software testing here individual units or components of a software are tested

example frameworks for unit testing:
jest, mocha, chai, jasmine, ...

we will use Jest (https://jestjs.io/)

npm install jest --save-dev
--save-dev since jest is only used to test program as part of development

1. Writing tests

    testing lib.js
    Conventionally, tests for <file_name>.js go to <file_name>.test.js
        lib.test.js

    const{ test, expect } = require("@jest/globals");
    const lib = require("./lib");

    test("sum([1, 2]) should be 3", () => {
        expect(lib.sum([1, 2])).toBe(3);
    })

    test("avg([1, 2]) should be 0", () => {
        expect(lib.avg([-5, 5])).toBe(0);
    })

    test("max([0, 3, 2]) should be 3", () => {
        expect(lib.max([0, 3, 2])).toBe(3);
    })

2. Linking Jest
open package.json and set "test" under "scripts" to "jest"

    "scripts": {
        "test": "jest"
    },

3. Running Test

npm test

CONGRATS! YOU FINISHED YOUR FIRST UNIT TESTING

WOOHOOOO YAYYYY WOWWWWWWW SHEEEEESSSSHHH HUMAYYYY BAAAAAAM


4. Main.js test
instead of checking the returned value of a function, we should run the script and check the actual output

the big picture
    1. Spawn to run a subprocess with the given command
    2. Store the printed strings to an array
    3. concatenate the strings and compare it with the expected output

    const {test, expect} = require("@jest/globals");
    const {spawn} = require("child_process");

    test("Insufficient params", () => {
        const main = spawn("node", ["main.js", "avg"]);
        const outputs = [];
        main.stdout.on("data", (output) => {
            outputs.push(output);
        });

        main.stdout.on("end", () => {
                const output = outputs.join("").trim();
                expect(output).toBe("Insufficient parameter!");
        });
    });

    test("Wrong command", () => {
        const main = spawn("node", ["main.js", "count", "0"]);
        const outputs = [];
        main.stdout.on("data", (output) => {
            outputs.push(output);
        });

        main.stdout.on("end", () => {
                const output = outputs.join("").trim();
                expect(output).toBe("Wrong command!");
        });

5. Code coverage
Ideally, each line of code should be executed at least once during testing

Code coverage: # of lines of code executed by test / total # of lines

6. Git actions
Time to push the code to Github
We want to make sure the unit tests automatically run every time we update the code
We can do this by GitHub Actions
    1. Open Action tab in repo
    2. Click on "Set up this workflow" under Node.js
        You can configure the workflow, but let's use the default
    3. Press "Start commit" and make a commit
        Configuration file is now added to your repo
        every new commit will trigger GitActions to run the tests on different versions of Node.js

7. Publishing the Project
npm publish

there may be errors since you are not logged in
    1. Sign up NPMJS (https://www.npmjs.com/)
    2. Finish email verification
    3. npm login
    4. npm publish
    5. Must increment version every time you publish (bump version)
    6. npm install <project_name> -g
        <project_name> is the project name in package.json