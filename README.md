# Infish

Infish stands for infinite shell. It's a way to maintain persistent shell access on a linux server even without ftp, ssh, or cpanel access. It works on all linux servers, even on shared hosting.

Note that this project is for **educational purposes** only. I bear no responsibility for how you use it. For this reason, no specific tutorial will be given for how exactly when or where to use this tool.

The aim of this shell is the give the penetration tester maximum and complete control over the system such that **only a reboot** can save the day. Infact if one has root access, one can set the script to run on boot, that way, the target is **screwed**.

# How it works
Here, you will have a shell that keeps checking on a paste on pastebin, and running whatever command it finds there. That way, you don't need access to the target machine. You've created a poor man's reverse shell, while remaining anonymous in the process.

Anytime you need to run a command, simply edit the paste to the command you want.

# Usage

Here are the steps. Follow them carefully.

- If you don't have an account, create one with paste bin.
- Create a new public paste and type in any shell command (One that won't make noise :)) then save.
- Edit your `.infish` by changing the value of the `url` variable in the `main` function to the **raw url** of your paste. Ensure it's the url to the **raw paste**.
- Upload the `.infish` file to a folder outside the web root directory. Find a good hiding place and rename it to something more benign, like `.cpanel_kernel`, but keep it as a dot file.
- If you can, fill the begining of the file with as much unneccesary bash code and comments as you can, to make it look legitimate.
- Finally run this command `nohup bash .infish & disown`


That's it, you own the server. If you have root access, you can set the last command to run on boot.

If you're confused or have no idea what's going on on this page, then you should not be here. Go build cute websites and apps.





Stay Dangerous :)
