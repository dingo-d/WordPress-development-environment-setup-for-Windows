# WordPress development environment setup for Windows

## Table of Contents

1. [Microsoft Web Platform](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#microsoft-web-platform)
2. [Composer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#composer)
3. [Node and linters](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#node-and-linters)
4. [Code Sniffer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#installing-php-code-sniffer)
  1. [WordPress Coding Standards](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#microsoft-web-platform)

======

#### Disclaimer

This document is meant for internal use, but if anybody stumbles upon it you can follow it and maybe you can benefit in some way. This is not anything official, and is meant as a guide to standardize the coding practices withing a company. Every developer has it's own way of doing things and this may not work for you. It works for me tho :D
I am not responsible for any data loss or such. But really it's justa a 'tutorial' of sorts, don't see how you could mess your system up.

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

### Node and linters

Download and run it. After installation you can go to command prompt and type:

```
npm install -g csslint
```

After that install jshint

```
npm install -g jshint
```

Your linters are ready to use, but we'll configure our SublimeText and code sniffer a bit later.

### Installing php code sniffer

We want to install php code sniffer next. The best way is to follow the instructions [here](https://github.com/squizlabs/PHP_CodeSniffer).

In the cmd prompt type

```
composer global require "squizlabs/php_code sniffer=*"
```

![composer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/composer.jpg)

To see if the code sniffer is installed you can type

```
phpcs -i
```

And you should see currently installed coding standards

```
The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz and Zend
```

Now we need to add WordPress Coding standards, because we are developing WordPress related stuff after all :D

#### WordPress Coding Standards

WPCS are set of rules that developers should follow so that lives of other developers would be easier. You can read about them on the [official page](https://make.wordpress.org/core/handbook/best-practices/coding-standards/).

Installing [WordPress Coding standards](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards) is easy as well.

Composer has our back on this one as well

```
composer create-project wp-coding-standards/wpcs:dev-master --no-dev
```

This will, however, install the wpcs in C:\ root in the wpcs\ directory and code sniffer won't pick it up on itself - this one I haven't tried, but the installation mentions that just running the above command will also install PHP_CodeSniffer and register the standards, so if you didn't install code sniffer first, and just ran this command it could be that the paths will be correctly set up and you won't really need to do much. But in the case that you've installed code sniffer alone first, you'll need to manually add the installed path for the WordPress coding standards

```
phpcs --config-set installed_paths C:wpcs\
```

After that running `phpcs -i` you should have in your cmd prompt

```
The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz, Zend, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and WordPress-VIP
```

##### Configuring the code sniffer

For our sniffer to work as we want it to work we need to set it up. We've already added installed paths. Now we need to add path to linters, and set up standards. For full documentation just [click here](https://github.com/squizlabs/PHP_CodeSniffer/wiki).

We'll need to find out where node put our linters. If you didn't change anything from the code so far (the one you type in command prompt), everything should be located in default places. So node should be in

```
%USERPROFILE%\AppData\Roaming\npm\node_modules\csslint
```

and

```
%USERPROFILE%\AppData\Roaming\npm\node_modules\jshint
```

Where `%USERPROFILE%` is just environment variable that points to your user folder.

So we can set up our sniffer. First define default standard. We're going to set it to WordPress. This will include WordPress-Core, WordPress-Extras, and WordPress-VIP standards as well. Some sniffs from WordPress-VIP won't be necessary if you're developing themes or plugins, but you can make your own exclusion list.

```
phpcs --config-set default_standard WordPress
```

If you're afraid that you've set something wrong you can easily check the config settings

```
phpcs --config-show
```

in my case I got out

```
default_standard: WordPress
installed_paths:  C:wpcs\
```

Let's move on.

