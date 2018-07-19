## Bash Redirection Cheatseet

## Useful Knowledge 

* Command line programs always have three "standard streams" available: Standard Input (stdin), Standard Output (stdout), Standard Error (stderr)

* Generally, the "good news" is in standard output and the "bad news" goes to stderr

* Each stream is associated with a number called a "File Descriptor" (1 stdout, 2 for stderr, 0 for stdin)

* The default for stdout & stderr is to display on the terminal

* Using the file-descriptor and some special syntax, the data in the stream can be "redirected" to another destination like a file, another program, or a black hole of sorts called /dev/null


## Redirecting Standard Output (stdout)

### Save output to a file stdout.txt

```sh
command 1>stdout.txt
command >stdout.txt # 1 is optional for stdout
```

### Append output to a file stdout.txt (no overwrite)

```sh
command 1>>stdout.txt
command >>stdout.txt # 1 is optional for stdout
```

### Discard output entirely (won't display on screen or persist to file)

```sh
command 1>/dev/null
command >/dev/null # 1 is optional for stdout
```

Notes:

- For stdout, you can safely drop the File Descriptor (1)

## Redirecting Standard Error (stderr)

Exact same syntax as above except the File Descriptor is mandatory: 

```sh
command 2>stderr.txt # Write stderr to file
command 2>>stderr.txt # Append errors to file
command 2>/dev/null # Discard stderr
```

Notes:

- Not all programs use stderr properly if at all

## Examples: Redirect stdout and stderr simultaneously

### Redirect to separate files:

```sh
command 1>stdout.txt 2>stderr.txt
command >stdout.txt 2>stderr.txt # 1 not needed
```


### Redirect to separate files (append, no overwrite):

```
command 1>>stdout.txt 2>>stderr.txt
command >>stdout.txt 2>>stderr.txt # 1 not needed
```

### Send stdout & stderr to the same place:

```sh
command >shared-output.txt 2>&1 # stdout to shared-output.txt, stderr to wherever stdout is going, here shared-output.txt

command 2>shared-output.txt >&2 # Same as above, just reversed, stdout to same spot as stderr

command 2>/dev/null >&2 # stderr discarded to /dev/null and stdout to same trashcan as stderr so it is discarded as well
```

### Append Shared Output (no overwrite):

```sh
command >>shared-output.txt 2>&1
```

Note above that stdout is appending to shared-output.txt and stderr is following File Descriptor 2 (so it will append as well)



Notes: 

- ORDER MATTERS! when using the & syntax above the order matters. Before "duplicating" a stream else you must first specify that stream's destination.


For example, this will not work as intended:

```sh
ls 2>&1 >shared-output.txt
```

In order what is happening: 

a. stderr is set to follow stdout, but stdout at that point is (by default) going to the terminal

b. stderr is therefore set to display in terminal

c. stdout is later redirected shared-output.txt

Any errors will go display on the terminal (probably not what we wanted) and stdout will be written to the file.

Note the difference between this working command and above:

```sh
ls >shared-output.txt 2>&1
```



### Practical Example: 


#### ex. npm install with errors/warnings to npm-errors.txt and all other output written to npm-output.txt

```sh
npm install >npm-output.txt 2>npm-errors.txt
```

#### ex. Completely silent npm install (discard all output & errors):
```sh
npm install >/dev/null 2>&1
```


## Standard Input & Piping



### Standard Input (stdin)

Like stdout and stderr, stdin can be "redirected." Stdin in the past was from keyboard but stdin to a program can come from anything-- a keyboard, a sensor, voice-to-text device, a file, another program's stdout, etc


```sh
command < file
```


### Ex. List files containing "json" in their filename

```
ls >files.txt # stdout to files.txt

grep json < files.txt # stdin to grep is from files.txt
```

The first command lists files but its stdout is *redirected* to files.txt. 

The second command receives files.txt as its stdin and then greps for records/files containing "json." Since ```grep``` itself is not being redirected, the list of ```*.json``` files will display in the terminal.



### Piping

Piping is very similar to redirecting to stdout but instead of writing it to a file, it gets redirected as the stdin of another program.

#### Ex. Pipe


Instead of writing above with two commands, we accomplish the same thing by piping:

```sh
ls | grep json
😎  ~/redirection-fun ls grep | json
1.json
2.json
3.json
4.json
5.json
6.json
```

The ls command lists files and then its stdout is then “piped” over as stdingrep json whose stdout is not being redirected so it displays in the terminal.

Notes: 





