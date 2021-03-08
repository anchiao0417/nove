---
timeToRead: 3
authors:
- Thiago Costa
title: 'How to solve Homebrew installation failure?  '
excerpt: 'xcode-select: error: invalid developer directory ''/Library/Developer/CommandLineTools'''
date: 2021-03-03T16:00:00+00:00
hero: "/images/homebrew.jpg"

---
```shell
    The operation couldn’t be completed. (NSURLErrorDomain error -1012.)
    ==> Installing the Command Line Tools (expect a GUI popup):
    ==> /usr/bin/sudo /usr/bin/xcode-select --install
    xcode-select: note: install requested for command line developer tools
    Press any key when the installation has completed.
    ==> /usr/bin/sudo /usr/bin/xcode-select --switch /Library/Developer/CommandLineTools
    xcode-select: error: invalid developer directory '/Library/Developer/CommandLineTools'
    Failed during: /usr/bin/sudo /usr/bin/xcode-select --switch /Library/Developer/CommandLineTools
```
If you get this error message while installing Homebrew, following my steps for troubleshooting!

First, try to download the CommandLineTool manually on [Apple Developer](https://developer.apple.com)

If you're able to log in and download the latest version of it, you should be good to go.

However, in my case, I get this message whenever I try to log in to the download page:

> We are unable to process your request. An unknown error occurred.

It's hard to get a clue of what makes it happen since it says 'unknown error'. I contacted Apple Customer service for help, unfortunately they couldn't address the problem. Apple should fix this problem seriously.

After some time of research, I found that CommandLineTools is installed if downloading the App 'Xcode' from Appstore, just note that in this way, the CommandLineTools might be in other directory, not as it should be in the homebrew install script.

So here we found the solution, copy the homebrew install script , then simply replace

**/Library/Developer/CommandLineTools**

to

**/Applications/Xcode.app/Contents/Developer**

You can also get this install file here in my [Github](https://github.com/anchiao0417/homebrew/blob/main/install.sh)

Download the script and cd to where it is, run it on the terminal
```shell
    ./install.sh
```
That's it! I believe this is because XCode's latest version has changed its installed path, however, Homebrew's install script still remains the old path which causes the problem.