# Hack Codegen [![Build Status](https://travis-ci.org/fredemmott/hack-codegen.svg?branch=master)](https://travis-ci.org/fredemmott/hack-codegen)
Hack Codegen is a library for easily generating Hack code and writing it
into signed files that prevent undesired modifications.
The idea behind writing code that writes code is to raise the level of
abstraction and reduce coupling.  You can use your own way of describing
a problem and generate the corresponding code.  E.g. see examples/dorm.
In this example, we use a schema to describe the structure of the data,
and we use Hack Codegen to write the matching code.

fredemmott/hack-codegen is derived from [facebookarchive/hack-codegen](https://github.com/facebookarchive/hack-codegen), which is no-longer supported by Facebook.

## Examples
The DORM example shows how to use the different aspects of the code
generation in a simplified real-life example.
The included tests also exemplify the usage of the different components.

## Requirements
Hack Codegen requires:
* HHVM
* Composer

## Installing Hack Codegen
This package can be installed via composer:

```bash
composer require fredemmott/hack-codegen
```

## Usage
Include the autoload file generated by composer and you are ready to start using it.
For example:

```php
<?hh
require 'vendor/autoload.php';

use Facebook\HackCodegen\HackCodegenFactory;

$cg = new HackCodegenFactory(new HackCodegenConfig());

echo $cg->codegenFile('HelloWorld.php')
  ->addClass(
    $cg->codegenClass('HelloWorld')
      ->addMethod(
        $cg->codegenMethod('sayHi')
          ->setReturnType('void')
          ->setBody('echo "hello world\n";')
      )
  )->save();

```

## Configuration
You can configure some options such as the maximum line width, spacing and
headers by subclassing `HackCodegenConfig.php` and passing a subclass to
`HackCodegenFactory`'s constructor.

## License
Hack Codegen is BSD-licensed. We also provide an additional patent grant.
