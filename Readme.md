# WordPress development environment setup for Windows

## Table of Contents

1. [Microsoft Web Platform](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#microsoft-web-platform)
2. [Composer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#composer)
3. [Node and linters](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#node-and-linters)
4. [Code Sniffer](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#installing-php-code-sniffer)
  1. [WordPress Coding Standards](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#microsoft-web-platform)
5. [Sublime Settings](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows#setting-up-sublimetext-for-development)


======

#### Disclaimer

This document is meant for internal use, but if anybody stumbles upon it you can follow it and maybe you can benefit in some way. This is not anything official, and is meant as a guide to standardize the coding practices withing a company. Every developer has it's own way of doing things and this may not work for you. It works for me tho :D
I am not responsible for any data loss or such. But really it's justa a 'tutorial' of sorts, don't see how you could mess your system up. The system I've used while testing this is Windows 10, but feel free to try anything from Windows 7 up.

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

Download node installation file and run it. After installation you can go to command prompt and install linters. First we'll install [csslint](https://github.com/SublimeLinter/SublimeLinter-csslint)

```
npm install -g csslint
```

After that install [jshint](https://github.com/SublimeLinter/SublimeLinter-jshint)

```
npm install -g jshint
```

And we'll also need [Rhino](https://github.com/mozilla/rhino) for our jshint to work.

```
npm install -g rhino
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

This will, however, install the wpcs in C:\ root in the \wpcs directory and code sniffer won't pick it up on itself - this one I haven't tried, but the installation mentions that just running the above command will also install PHP_CodeSniffer and register the standards, so if you didn't install code sniffer first, and just ran this command it could be that the paths will be correctly set up and you won't really need to do much. But in the case that you've installed code sniffer alone first, you'll need to manually add the installed path for the WordPress coding standards

```
phpcs --config-set installed_paths C:wpcs
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
installed_paths:  C:wpcs
```

Let's move on. We'll add option to show progress

```
phpcs --config-set show_progress 1
```

I wanted to add colors, but if you have Anniversary edition of Windows 10 installed, the colors in cmd prompt won't work, because MS team removed them (why they did that is a complete mistery to me).

Next set the encoding

```
phpcs --config-set encoding utf-8
```

Tab width - the default tab width must be 4, and WordPress .php files must use tabs for indentations. Spaces are not allowed.

```
phpcs --config-set tab_width 4
```

Now we can set the lint paths

```
phpcs --config-set csslint_path %USERPROFILE%\AppData\Roaming\npm\node_modules\csslint
phpcs --config-set jshint_path %USERPROFILE%\AppData\Roaming\npm\node_modules\jshint\dist\jshint.js
phpcs --config-set rhino_path %USERPROFILE%\AppData\Roaming\npm\node_modules\rhino
```

With that, our code sniffer should be ready to use from the command prompt. But this is something we'll only use to check in the end to generate a [report](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Reporting).

So how does it look when you run it from the command prompt? Kinda like this:

![cmd sniff](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/sniff_example.jpg)

##### Note

If you're code sniffing an entire theme it's good to specify the extensions you wish to sniff. In case of WordPress we don't need to check `.html`, `.po`, `.pot` or any image files, so you can set the valid extensions with

```
phpcs --extensions=php,js,css /path/to/code
```

Additionally you can ignore files or folders

```
phpcs --ignore=*/tests/*,*/data/* /path/to/code
```

Also some minor errors can be [automatically fixed](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically).

### Setting up SublimeText for development

SublimeText 3 is awesome. What makes it awesome are all the extensions. Ones I'm using are

* Alignment
* CSS ToC
* DeleteBlankLines
* DocBlockr
* Emmet
* Emmet Css Snippets
* Increment Selection
* Javascript Console
* Nodejs
* SublimeLinter
* SublimeLinter - csslint
* SublimeLinter - jshint
* SublimeLinter - phpcs

The last three are the ones that are most important. For them to work we need to set it up. Install them using Package Manager.

First of all we can look at my default settings that you can get by going to `Preference > Settings`

```json
{
	"always_show_minimap_viewport": true,
	"auto_upgrade": false,
	"bold_folder_labels": false,
	"detect_indentation": true,
	"font_options":
	[
		"gray_antialias",
		"subpixel_antialias"
	],
	"font_size": 13,
	"ignored_packages":
	[
		"Autoprefixer",
		"BracketHighlighter",
		"Vintage"
	],
	"indent_guide_options":
	[
		"draw_normal",
		"draw_active"
	],
	"line_padding_bottom": 1,
	"line_padding_top": 1,
	"material_theme_disable_fileicons": false,
	"overlay_scroll_bars": "enabled",
	"tab_size": 4,
	"translate_tabs_to_spaces": false,
	"trim_trailing_white_space_on_save": true,
	"word_wrap": true
}

```

Besides that I also have

```json
	"color_scheme": "Packages/Material Theme/schemes/Material-Theme-Darker.tmTheme",
	"theme": "Material-Theme-Darker.sublime-theme",
```

But you need to install [Material Theme](https://github.com/equinusocio/material-theme) first. It's up to you. Next we need to set up our linters and sniffer. I'm using linter to handle the code sniffing too. Go to `Preferences > Package Settings > SublimeLinter > User Settings` and set it up like this

```json
{
    "user": {
        "debug": false,
        "delay": 0.25,
        "error_color": "cd3227",
        "gutter_theme": "Packages/SublimeLinter/gutter-themes/Default/Default.gutter-theme",
        "gutter_theme_excludes": [],
        "lint_mode": "background",
        "linters": {
            "csslint": {
                "@disable": false,
                "args": [],
                "box-sizing": false,
                "errors": "",
                "excludes": [],
                "ignore": [
                    "outline-none",
                    "box-sizing",
                    "ids",
                    "adjoining-classes",
                    "floats",
                    "qualified-headings",
                    "unique-headings",
                    "important",
                    "universal-selector",
                    "box-model",
                    "font-faces",
                    "font-sizes"
                ],
                "warnings": ""
            },
            "eslint": {
                "@disable": true,
                "args": [],
                "excludes": []
            },
            "jscs": {
                "@disable": true,
                "args": [],
                "excludes": []
            },
            "jshint": {
                "@disable": false,
                "args": [],
                "excludes": [],
                "tab_size": 4
            },
            "jslint": {
                "@disable": true,
                "args": [],
                "excludes": []
            },
            "php": {
                "@disable": false,
                "args": [],
                "excludes": []
            },
            "phpcs": {
                "@disable": false,
                "args": [],
                "excludes": [],
                "standard": "WordPress"
            },
            "pylint": {
                "@disable": false,
                "args": [],
                "disable": "",
                "enable": "",
                "excludes": [],
                "paths": [],
                "rcfile": "",
                "show-codes": false
            }
        },
        "mark_style": "outline",
        "no_column_highlights_line": false,
        "passive_warnings": false,
        "paths": {
            "linux": [],
            "osx": [],
            "windows": []
        },
        "python_paths": {
            "linux": [],
            "osx": [],
            "windows": []
        },
        "rc_search_limit": 3,
        "shell_timeout": 10,
        "show_errors_on_save": false,
        "show_marks_in_minimap": true,
        "syntax_map": {
            "html (django)": "html",
            "html (rails)": "html",
            "html 5": "html",
            "php": "html",
            "python django": "python"
        },
        "warning_color": "66cc33",
        "wrap_find": true
    }
}
```

You'll notice that I've set up some settings in ignore for csslint. Those are mostly warnings or 'errors' that you can safely ignore. After you've set this all up, restart the Sublime to give it a chance to load all the settings you've now set up.

How does our code sniffer looks like in Sublime? Like this

![sublime code sniff jshint](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/sublime_sniff.jpg)

Here I've purposefully removed a comma from a JavaScript code, and I immediately got an error which shows in the bottom left corner of the sublime, with red dot on the numbers. This is a linter error. A phpcs errors look like this

![sublime code sniff php](https://github.com/dingo-d/WordPress-development-environment-setup-for-Windows/blob/master/images/sublime_sniff2.jpg)
