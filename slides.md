## Say Hi to JOHN

![JohnWaving](JohnWaving.jpeg)

---

John wants to do a good job in his Digital Organization class.
But he doesn't understand what is happening on his MacBook.

Let's help John out.

---

## What is zsh?

John has found the Terminal on his Mac. The first thing he reads is:
```
The default interactive shell is now zsh.
To update your account to use zsh, please run
`chsh -s /bin/zsh`.
```
- zsh or Z shell (bash: prior to macOs Catalina)
- shell = program that interprets your Terminal commands for the operating system (aka command-line interpreter)
- interactive = you interact by telling the computer what you want through commands

---
## Running into Problems
~~~
John:~ john$ /Users/john/Desktop/DO-CLASS
-bash: /Users/john/Desktop/DO-CLASS: is a directory
>npm install -g reveal-md
>sudo npm install -g reveal-md
>reveal-md -v
-bash: -v: command not found
~~~
**Problem 1: John wasn't in the correct directory.**
```
John:~ john$ cd /Users/john/Desktop/DO-CLASS
```
---

![JohnHeadscratch](JohnHeadscratch.jpeg)

---
## Some important inputs

> **cd** = change directory

> **sudo** = run command as superuser

> **npm** = Node Package Manager

> **install -g** = global install (module is accessible from any project)

---

> **node.js** = open-source, Javascript runtime environment

> **reveal.js** = free open source HTML presentation framework 

> **reveal-md** = using Markdown (instead of HTML) to create presentations


---
## Slides won't open
John is in the correct directory. He has installed npm, reveal-md and node but...
~~~~
Johns:~ john$ cd /Users/john/Desktop/DO-CLASS
[Johns-MacBook:DO-CLASS john$ >npm install -g reveal-md
usage: install [...]
[Johns-MacBook:DO-CLASS john$ node -v
v.12.18.3
[Johns-MacBook:DO-CLASS john$ npm -v
6.14.6
[Johns-MacBook:DO-CLASS john$ reveal-md slides.md
-bash: -v: command not found
~~~~
...his slides still won't open.

---

![JohnShoulderShrug](JohnShoulderShrug.jpeg)

---
## Solving John's Problem
Finally, he uses npx and **it works**...

- **npx** = npm package runner
--> it works because it doesn't matter where or if you've installed reveal-md.
--> npx will temporarily install it and run it.
```
[Johns-MacBook:DO-CLASS john$ npx reveal-md slides.md
Downloading Chromium r674921 - 108.3 Mb [==========] 100% 0.0s
```
...**but now** every time he wants to open his slides, John has to wait **ages** for the download to complete.

---
## Solving John's Problem continued
Where is the reveal-md File saved?
```
/Users/john/.npm-global/bin/reveal-md
```
John has found the correct path to his slides. NPM stores its packages in the hidden files on MaBook. John does not have permission to write to these directories.

---

**bin** = binary file --> composed of something other than human-readable text

---

**Problem 2: Hidden files and Mac Permissions**

---
## Hidden Files
To see hidden files on Mac:
1. John opens Users in Macintosh HD via Spotlight Search (e.g.users/john)

2. He presses Command+Shift+Dot

3. John's hidden files become visible.

4. Undo reveal by repeating step 2

---

## Important commands for fixing Permissions
> **PATH**
(=variable) tells the shell which directories to search for ready-to-run programs

> **export command**
makes environment variables available to other programs 

---

> **echo $PATH**
the dollar preceding PATH tells echo to repeat the value of the variable PATH 

---

## To circumvent Mac Permissions:
John has to configure his directory (DO-Class) 
to run reveal-md by making it's absolute path available 
```
[Johns-MacBook:DO-CLASS john$
> /Users/john/.npm-global/bin/reveal-md
> export PATH=~/.npm-global/bin:$PATH
> echo $PATH
/Users/john/.npm-global/bin:/usr/local/bin:
/usr/bin:/bin:/usr/sbin:/sbin
> reveal-md
[Usage: cli <slides.md> [options]
See https://github.com/webpro/reveal-md for more details.
```

---

## Reveal-md Options
```
  -V, --version                               output the version number
      --title <title>                         Title of the presentation
  -s, --separator <separator>                 Slide separator [default: 3 dashes (---) surrounded by two blank lines]
  -S, --vertical-separator <separator>        Vertical slide separator [default: 4 dashes (----) surrounded by two blank lines]
  -t, --theme <theme>                         Theme [default: black]
      --highlight-theme <theme>               Highlight theme [default: zenburn]
      --css <files>                           CSS files to inject into the page
      --scripts <files>                       Scripts to inject into the page
      --assets-dir <dirname>                  Defines assets directory name [default: _assets]
      --preprocessor <script>                 Markdown preprocessor script
      --template <filename>                   Template file for reveal.js
      --listing-template <filename>           Template file for listing
      --glob <pattern>                        Glob pattern to select markdown files for listing and conversion [default: **/*.md]
      --print [filename]                      Print to PDF file
      --static [dir]                          Export static html to directory [_static]. Incompatible with --print.
      --static-dirs <dirs>                    Extra directories to copy into static directory. Only used in conjunction with --static.
  -w, --watch                                 Watch for changes in markdown file and livereload presentation
      --disable-auto-open                     Disable auto-opening your web browser
      --host <host>                           Host [default: localhost]
      --port <port>                           Port [default: 1948]
      --featured-slide <num>                  Capture snapshot from this slide (numbering starts from 1) and use it as og:image for static build. Defaults to first slide. Only used with --static.
      --absolute-url <url>                    Define url used for hosting static build. This is included in OpenGraph metadata. Only used with --static.
      --print-size                            Paper size to use in exported PDF files
      --puppeteer-launch-args <args>          Customize how Puppeteer launches Chromium. The arguments are specified as a space separated list (for example --puppeteer-launch-args="--no-sandbox --disable-dev-shm-usage"). Needed for some CI setups.
      --puppeteer-chromium-executable <path>  Customize which Chromium executable puppeteer will launch. Allows to use a globally installed version of Chromium.
  -h, --help                                  output usage information
```
---
## ls -la
```
Johns-MacBook:DO-CLASS john$ ls -la
total 32
drwxr-xr-x@  5 john  staff   160 Oct  1 15:25 .
drwx------@ 17 john  staff   544 Oct  1 15:25 ..
-rw-r--r--@  1 john  staff  6148 Sep 17 14:25 .DS_Store
-rw-r--r--   1 john  staff   125 Sep 17 14:12 mdtrial.md
-rw-r--r--@  1 john  staff  2227 Oct  1 15:25 slides.md
```
ls = list
la = long

---
## Solution
John now goes into the directory where slides.md is.
```
cd /Users/john/Desktop/DO-CLASS
```
He makes the path of reveal-md available for his directory.
```
export PATH=~/.npm-global/bin:$PATH
```
John can finally open his slides with a short command procedure.
```
reveal-md slides.md -w
Reveal-server started at http://localhost:1948
```
---
## Thank you for Listening

![JohnLightBulb](JohnLightBulb.jpeg)

---

### Sources
##### Warren, T. (2019). Apple replaces bash with zsh as the default shell in macOS Catalina. Retrieved 02/10/20 from https://www.theverge.com/2019/6/4/18651872/apple-macos-catalina-zsh-bash-shell-replacement-features

##### Apple Support (2020). Use zsh as the default shell on your Mac. Retrieved 02/10/20 from https://support.apple.com/en-us/HT208050

##### Jones,M. (2011). Evolution of shells in Linux. Retrieved 02/10/20 from https://developer.ibm.com/tutorials/l-linux-shells/#artrelatedtopics

##### NPM (2020). A Note on Permissions. Retrieved 02/10/20 from http://npm.github.io/installation-setup-docs/installing/a-note-on-permissions.html

---

##### Nodejs.org (2011). What is npm. Retrieved 02/10/20 from https://nodejs.org/en/knowledge/getting-started/npm/what-is-npm/

##### The Linux Information Project (2007). Retrieved 02/10/20 from http://www.linfo.org/path_env_var.html

