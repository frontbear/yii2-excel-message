# WIP This extension is still considered alpha stage!

Please use at your own risk - and leave feedback so that we can improve it! Thanks!

Yii2 Excel Message
==================

[![Latest Stable Version](https://poser.pugx.org/codemix/yii2-excel-message/v/stable.svg)](https://packagist.org/packages/codemix/yii2-excel-message)
[![Total Downloads](https://poser.pugx.org/codemix/yii2-excel-message/downloads)](https://packagist.org/packages/codemix/yii2-excel-message)
[![Latest Unstable Version](https://poser.pugx.org/codemix/yii2-excel-message/v/unstable.svg)](https://packagist.org/packages/codemix/yii2-excel-message)
[![HHVM Status](http://hhvm.h4cc.de/badge/yiisoft/yii2-dev.png)](http://hhvm.h4cc.de/package/codemix/yii2-excel-message)
[![License](https://poser.pugx.org/codemix/yii2-excel-message/license.svg)](https://packagist.org/packages/codemix/yii2-excel-message)


Translate new messages via Excel files.


## Features

With this extension you can export your new messages from PHP message files to
Excel, send them to your translators and read them back in to update your
message files.

To read and write to and from Excel file, we use the excellent
[PHPExcel](https://github.com/PHPOffice/PHPExcel) package.


## Installation

Install the package through [composer](http://getcomposer.org):

    composer require codemix/yii2-excel-message@dev

And then add this to your console application configuration:

```php
<?php
return [
    'controllerMap' => [
        'excel-message' => [
            'class' => 'codemix\excelmessage\ExcelMessageController'
        ]
    ]
];
```

Now you're ready to use the extension.


## Creating Excel files with new translations

To create Excel files with new  translations, you need to supply the message
configuration and the output directory where the files should be written to:

```
./yii excel-message messages/config.php /output/dir
```

This will create one file per language with one sheet per category each. The
source messages are listed in column `A` and the translations can then be added
to column `B`.

The files will be in `Excel2007` format with `xlsx` extension.

If you want a file with all translations instead, pass `all` as 3rd argument.

> Note: You must use 'php' as `format` in your message configuration.

## Update PHP message files from Excel files

To update your existing message files from the updated Excel files you
again need to supply the message configuration and the directory path
where your Excel files reside:

```
./yii excel-message/import messages/config.php /input/dir
```

Now the new translations have been added to your PHP message files. Yes it's
really that simple.

You should use the same file organisation as when creating the file: One file
per language with language code as filename, one sheet per category, source
messages in column `A`, translations in column `B`, first line is skipped.

You can also pass a third parameter with the file extension. Default is `xlsx` -
but PHPExcel should also autodetect other Excel formats 

## Options

You can use the following options.

Option  | Description
------- | -----------
`--languages=aa,bb,cc` | Comma separated list of languages to process.
`--categories=cat1,cat2` | Comma separated list of categories to process.
`--ignoreLanguages=aa,bb,cc` | Comma separated list of languages to ignore. This option is ignored if `--languages` is used.
`--ignoreCategories=cat1,cat2` | Comma separated list of categories to ignore. This option is ignored if `--categories` is used.
`--lineHeight=x` | `export` only: The line height to set on the excel file. The default is *auto* but this [does not work](https://github.com/PHPOffice/PHPExcel/issues/588) if the file is openend in LibreOffice Calc. So you can set a fixed line height like `50` here as a workaround.
