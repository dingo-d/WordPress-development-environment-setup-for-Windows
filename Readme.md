# WordPress development environment setup for Windows

======

## Prerequisites

**Clean slate** - remove any xampp, composer, pear, php or anything you had on your Windows machine

**Install Node.js** - https://nodejs.org/en/
We'll need it for our linters

**SublimeText 3** - https://www.sublimetext.com/3
Favorite text editor \o/

**Composer** - https://getcomposer.org/download/
A dependency management for PHP

**Microsoft Web Platform Installer** - https://www.microsoft.com/web/downloads/platform.aspx
PHP for Windows!

### Delete all things!
======

First you need to have a clean system - clean from any previous installations of php on your computer - in a form of php, xampp or any other tool that allows you to
work with php. The less previous 'stuff' on your computer there is, the easier this process will be :)

======

### Microsoft Web Platform

Go to https://www.microsoft.com/web/downloads/platform.aspx and download the web platform. After installation in Search type in php, and you'll see many versions of php that you'll need to install.

![web platform installer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/MSWebPlatform.jpg)

Run the installer as Administrator.

Install latest php version (7.0.9) for your type of Windows (x86 for 32-bit and x64 for 64-bit). If there are any kind of issues - download version 5.6.24.

Run command prompt (cmd) and type:

```
C:\>php -v
```

You should see something like this

![php inside your command prompt](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/cmd_php.jpg)

This means that we have php on our Windows. Cool. Restart your computer for good measure.

### Composer