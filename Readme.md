# WordPress development environment setup for Windows

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
php -v
```

You should see something like this

![php inside your command prompt](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/cmd_php.jpg)

This means that we have php on our Windows. Cool. Restart your computer for good measure.

### Composer

Now that we have php we can install it from our cmd prompt. But it's easier to just download the installer and run it. So do it. It will find the php path for you. The proxy server **shouldn't** be clicked (for our purposes). Click next untill it's installed.
Restart for a good measure. You could just log off and on, but it's safer just to restart.

#### Installing php code sniffers

We want to install php code sniffer next. The best way is to follow the instructions [here](https://github.com/squizlabs/PHP_CodeSniffer).

In the cmd prompt type

```
composer global require "squizlabs/php_codesniffer=*"
```

### Node.js

Download and run it. After installation you can go to command prompt and type:

```
npm install -g csslint
```

After that install jshint

```
npm install -g jshint
```

