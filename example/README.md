## Bash redirection

Does the following look confusing?

```sh

/dev/bin myapp >logfile 2>&1

```

Companion blog post here: [link]()


Shorter cheat-sheet version here: [link](../cheatsheet.md) 

Once you've read the above, try the example below: 

## npm example

If you have [nodejs](https://nodejs.org/en/) installed your machine you should have access to its package manger, [https://www.npmjs.com/](npm)


Since npm can be a very noisy tool, here's an opportunity to use your new skills to attempt the following:


- [ ] Run ```npm install``` with stdout redirected to stdout.txt

- [ ] Run ```node index.js``` on its own, then redirect stdout to stdout.txt

- [ ] Run ```npm start``` and write stdout it to stdout.txt

- [ ] Run ```npm run error``` and redirect stderr to errors.txt and let any other output display on screen

- [ ] Run ```npm run error``` but redirect BOTH stdout and stderr errors.txt but do not overwrite (multiple runs should add latest stdout/stderr to the bottom of the file)


Once you've tried the above, take a peek at [solutions.md](./solutions.md)