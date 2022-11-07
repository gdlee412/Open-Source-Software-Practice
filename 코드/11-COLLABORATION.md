# Collaboration

## Markdown
a lightweight markup language that you can use to format text documents.
    much simpler than HTML

Used everywhere in Github (md) e.g, documentation, issues, pull requests, etc

Heading, lists, tables, images, links, ...

https://guides.github.com/features/mastering-markdown/

https://www.markdownguide.org/basic-syntax

```html
<!--REPRESENTATIONS-->
<h1> = #
<h2> = ##
<h3> = ###
...

<strong> = ** ** between (2 pairs of asterisks)
<em> = * * between (a pair of asterisks)
<ul> <li> = - 
<ol> <li> = 1.

<a href> = [Word here](link here)
```

```c
//```(language here)
code here
printf("Hello");
//```
```

## Owner vs Collaborators
- Owner: the user who created a repository
- you can invite collaborators to your repo as you want
    - settings -> manage access
-  Things that both the owner and collaborators can do:
    - Pull the content (read)
    - Push changes (write)
    - Rename a branch
    - Create, assign, close, and re-open issues
    - Create, merge, and close pull requests
    - ...almost everything that you do to maintain the repository
- Things that the owner can do but collaborators cannot do:
    - Invite collaborators
    - Change the visibility of the repo (e.g., public -> private)
    - Delete the repo
    - Manage security settings
- In your project, one of your team member should be an owner and invite others to the repo

## External Contributors
- external contributors:
    - Contribute to an open-source project without being invited as a collaborator

1. Fork the target repo to your account
2. Modify your repo
3. Write a pull request
4. The collaborators of the original repo will approve your pull request


## Forking a Repository
- forking a repo will get you a clone of the original repo under your account
    - e.g., d3/d3 becomes e-/d3
- You are the owner of the repo, so you can do anything, e.g., commiting changes

## Creating a Pull Request
- Changes made in the forked repo are not visible in the original repo
- To reflect the changes on the original repo, you need to create a **pull request** to the original repo
- **Pull Request**: "Please review what I have done and merge the changes if you like"

```
1. User A creates a repo A/skku-stat.
2. User B forks the repo as B/skku-stat.
3. User B clones B/skku-stat into B's local machine.
4. User B makes changes and push them to B/skku-stat.
    - git commit and git push
5. User B goes to the "Pull requests" tab of A/skku-stat.
6. User B clicks on "New pull request".
7. User B clicks on "Compare across forks".
    - Left: A's branch into which B wants to merge B's.
    - Right: B's branch (newer)
    - Diff view below shows the changes
8. User B clicks on "Create pull request".
    - Leave a message so that the owner and collaborators of the repo can understand what you did
        - Use the markdown syntax
9. GitHub automatically runs the tests the repo has and checks merge conflicts.
10. You can discuss with the maintainers (owner or collaborators)
    - maybe they require some changes
11. User A finds the pull request that User B left and comments on it.
12. User B modifies the source code again.
13. The additional changes that User B made is automatically reflected on the old pull request.
    - No need to remove the old one and create a new one.
14. User A clicks on "Merge pull request".
15. B's code has been applied to A's repo.
```

## Issue Management
- Go to "Issues" tab
- Use Markdown
- You can notify a user using @(username).
- Assign to a special user (maintainers only).
- Labels are very useful. Categorize the issues (maintainers only).
- Issues and pull requests are closely related.
```
1. User C reports a bug as an issue.
2. User B fixes the issue and creates a pull request.
3. User A approves the pull request.
```
- You can re-open or close a relevant issue in a pull request message.

## Code review
- to ensure the code quality, you can enforce people to do code review before merging a pull request.
- Settings -> Branches -> Branch protection rules
- Make at least one reviewer review the pull request before merging it
- Set the branch name pattern to "main".
- Before a reviewer approves a pull request, you cannot merge the pull request

1. To review the pull request, go to the "File changed" tab
2. You can comment on the files changed line by line
3. If you are done, finish the review by approving the requested changes
- To make your pull request approved:
    - Pass all tests
    - No merge conflicts
    - Receive an enough number of reviews

## Documentation
- To make your code accessible by others, documentation is a must
    - Usually written in README.md using Markdown

```
- A brief overview
- Links to resources
- Installation
- API reference
- Examples
- Releases (versions)
- How to contribute
- License
- Code of Conduct
```

- You can embed documentation in the code.
- e.g., jsdoc (https://jsdoc.app/)

```js
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book
 * @param {string} author - The author of the book
 */
function Book(title, author) {}
```

## Tips for Documentation
- Apply formatting (Markdown!)
    - Readable and consistent
- Provide quick start instructions
- Provide examples (with expected outputs)
- Document how to document
- COde of conduct
- A feedback mechanism
- An issue template

## Code of Conduct
- Safe work environments
- Mutual respect
- Empathy and kindness
- Constructive feedback
- No trolling, insulting, harassment, etc.
- Microsoft's Code of Conduct
    - https://opensource.microsoft.com/codeofconduct/

## Issue Templates
- Use a consistent format for issues or bug reports
- Settings -> Options -> Features

## License
- **License**: a legal instrument governing the use or redistribution of software.
    - Usually in LICENSE file in a repo
    - Commercial use
    - Modification
    - Distribution
    - Private use
    - Liability
    - Warranty
- You can include a LICENSE file when you create a repo
- https://choosealicense.com/
- The MIT license is one of the most permissive licenses
- Some licenses require you to use the same license for modified code when you release your software to public.
    - GNU GPLv3, GNU LGPLv3, ...
- Be careful when you use code under these licenses.
    - You must disclose your source!
    - Software under GPL: Git, MariaDB, MySQL, Notepad++, ...

# Summary: Collaboration
- **Markdown** is a simple markup language for documents in GitHub
    - Issues/pull requests/documentation/...
- External collaborators contribute to open-source projects by making **fork and pull requests**.
- Issue management and code review 
- Document your source code to make it reusable.
- **License**: commercial use/modification/distribution/liability/warranty

## Can you figure out what the following files/directories do?
1. .github/workflows
2. .git
3. .editorconfig
4. .gitignore
5. ISSUE_TEMPLATE
6. LICENSE.md
7. main.js
8. package.json
9. README.md
10. node_modules