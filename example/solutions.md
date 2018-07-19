## npm example [answers]


- [ ] Run ```npm install``` with stdout redirected to stdout.txt

```sh
npm install >stdout.txt

```

Notes: Notice that when redirecting stdout, the command otherwise functions normally just the plaintext is redirected to a file


- [ ] Run ```node index.js``` on its own, then redirect stdout to stdout.txt

```sh
node index.js
node index.js >stdout.txt

```

Notes: Note that stdout doesn't take color information with it, just plaintext

- [ ] Run ```npm start``` and write stdout it to stdout.txt

```sh
npm start >stdout.txt

```

Notes: If you inspect stdout in this case, it will have both the simple node program's output alongside the boilerplate from NPM


- [ ] Run ```npm run error``` and redirect stderr to errors.txt and let any other output display on screen

```sh
npm run error 2>errors.txt
```

- [ ] Run ```npm run error``` but redirect BOTH stdout and stderr errors.txt but do not overwrite (multiple runs should add latest stdout/stderr to the bottom of the file)

```sh

npm run error 2>>errors.txt 1>&2
```

Notes: We explicitly redirect STDERR to append mode and then redirect STDOUT to STDERR's destination

These commands are functionally equivalent: 

```sh
npm run error >>errors.txt 2>&1 # Set stdout to errors.txt in append mode, stderr to stdout's destination
npm run error >>errors.txt 2>>errors.txt # Set stdout to append errors.txt and stderr to append errors.txt

````

