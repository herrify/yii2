Debug Extension for Yii 2
=========================

This extension provides a debugger for Yii 2 applications. When this extension is used,
a debugger toolbar will appear at the bottom of every page. The extension also provides
a set of standalone pages to display more detailed debug information.

<<<<<<< HEAD
This repository is a git submodule of <https://github.com/yiisoft/yii2>.
Please submit issue reports and pull requests to the main repository.
For license information check the [LICENSE](LICENSE.md)-file.
=======
>>>>>>> yiichina/master

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
<<<<<<< HEAD
php composer.phar require --prefer-dist yiisoft/yii2-debug
=======
php composer.phar require --prefer-dist yiisoft/yii2-debug "*"
>>>>>>> yiichina/master
```

or add

```
<<<<<<< HEAD
"yiisoft/yii2-debug": "~2.0.0"
=======
"yiisoft/yii2-debug": "*"
>>>>>>> yiichina/master
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply modify your application configuration as follows:

```php
return [
    'bootstrap' => ['debug'],
    'modules' => [
        'debug' => 'yii\debug\Module',
        // ...
    ],
    ...
];
```

You will see a debugger toolbar showing at the bottom of every page of your application.
You can click on the toolbar to see more detailed debug information.
