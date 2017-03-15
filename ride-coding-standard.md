# Ride Coding Standard

This standard is based on the PSR standards with some changes.
All changes are marked in bold to have a quick overview where this standard does 
not follow the PSR standards.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

## 1. PSR-0: Autoloading Standard

The following describes the mandatory requirements that must be adhered
to for autoloader interoperability.

### 1.1 Mandatory

* A fully-qualified namespace and class must have the following
  structure `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* Each namespace must have a top-level namespace ("Vendor Name").
* Each namespace can have as many sub-namespaces as it wishes.
* Each namespace separator is converted to a `DIRECTORY_SEPARATOR` when
  loading from the file system.
* Each `_` character in the CLASS NAME is converted to a
  `DIRECTORY_SEPARATOR`. The `_` character has no special meaning in the
  namespace.
* The fully-qualified namespace and class are suffixed with `.php` when
  loading from the file system.
* __Alphabetic characters in vendor names, namespaces must be in lower case. 
For class names they must be in StudlyCaps.__

### 1.2 Example

* `\ride\library\AutoLoader` => `/path/to/project/vendor/ride/library/AutoLoader.php`

### 1.3 Underscores in Namespaces and Class Names

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

The standards we set here should be the lowest common denominator for
painless autoloader interoperability. You can test that you are
following these standards by utilizing this sample SplClassLoader
implementation which is able to load PHP 5.3 classes.

## 2. PSR-1: Basic Coding Standard

This section of the standard comprises what should be considered the standard
coding elements that are required to ensure a high level of technical
interoperability between shared PHP code.

### 2.1. Overview

- Files MUST use only `<?php` and `<?=` tags.
- Files MUST use only UTF-8 without BOM for PHP code.
- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but SHOULD NOT do both.
- Namespaces and classes MUST follow __PSR-0__.
- Class names MUST be declared in `StudlyCaps`.
- Class constants MUST be declared in all upper case with underscore separators.
- Method names MUST be declared in `camelCase`.

### 2.2. Files

#### 2.2.1. PHP Tags

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

#### 2.2.2. Character Encoding

PHP code MUST use only UTF-8 without BOM.

#### 2.2.3. Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

~~~php
<?php

// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo() {
    // function body
}
~~~

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

~~~php
<?php

// declaration
function foo() {
    // function body
}

// conditional declaration is *not* a side effect
if (!function_exists('bar')) {
    function bar() {
        // function body
    }
}
~~~

### 2.3. Namespace and Class Names

Namespaces and classes MUST follow __the "autoloading" [PSR-0]__.

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

Class names MUST be declared in `StudlyCaps`.

Code MUST use formal namespaces.

For example:

~~~php
<?php

namespace Vendor\Model;

class Foo {

}
~~~

### 2.4. Class Constants, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

__NOTE: Use meaningfull names. Sometimes it's better to use a longer, meaningful name, then a shorter meaningless name.__

#### 2.4.1. Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

~~~php
<?php

namespace Vendor\Model;

class Foo {

    const VERSION = '1.0';
    
    const DATE_APPROVED = '2012-06-01';
    
}
~~~

__NOTE: It's advised to use a prefix to indicate what kind of constant it is (eg. PARAM_XXX).__

#### 2.4.2. Properties

__Properties MUST be declared in `$camelCase`.__

#### 2.4.3. Methods

Method names MUST be declared in `camelCase()`.

## 3. PSR-2: Coding Style Guide

This guide extends and expands on [PSR-1], the basic coding standard.

The intent of this guide is to reduce cognitive friction when scanning code
from different authors. It does so by enumerating a shared set of rules and
expectations about how to format PHP code.

The style rules herein are derived from commonalities among the various member
projects. When various authors collaborate across multiple projects, it helps
to have one set of guidelines to be used among all those projects. Thus, the
benefit of this guide is not in the rules themselves, but in the sharing of
those rules.

### 3.1. Overview

- Code MUST follow a "coding style guide" PSR [[PSR-1]].
- Code MUST use 4 spaces for indenting, not tabs.
- There MUST NOT be a hard limit on line length; the soft limit MUST be 120
  characters; lines SHOULD be 80 characters or less.
- There MUST be one blank line after the `namespace` declaration, and there
  MUST be one blank line after the block of `use` declarations.
- Opening braces for classes MUST go on __the same line__, and closing braces MUST
  go on the next line after the body.
- Opening braces for methods MUST go on __the same line__, and closing braces MUST
  go on the next line after the body.
- Visibility MUST be declared on all properties and methods; `abstract` and
  `final` MUST be declared before the visibility; `static` MUST be declared
  after the visibility.
- Control structure keywords MUST have one space after them; method and
  function calls MUST NOT.
- Opening braces for control structures MUST go on the same line, and closing
  braces MUST go on the next line after the body.
- Opening parentheses for control structures MUST NOT have a space after them,
  and closing parentheses for control structures MUST NOT have a space before.

#### 3.1.1. Example

This example encompasses some of the rules below as a quick overview:

~~~php
<?php

namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface {

    public function sampleMethod($a, $b = null) {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar() {
        // method body
    }
    
}
~~~

### 3.2. General

#### 3.2.1. Basic Coding Standard

Code MUST follow all rules outlined in [PSR-1].

#### 3.2.2. Files

All PHP files MUST use the Unix LF (linefeed) line ending.

All PHP files MUST end with a single blank line.

The closing `?>` tag MUST be omitted from files containing only PHP.

__The opening `<?php`tag MUST be succeeded by a blank line.__

#### 3.2.3. Lines

There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers
MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD
be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

Blank lines MAY be added to improve readability and to indicate related
blocks of code.

There MUST NOT be more than one statement per line.

#### 3.2.4. Indenting

Code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.

> N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid
> problems with diffs, patches, history, and annotations. The use of spaces
> also makes it easy to insert fine-grained sub-indentation for inter-line
> alignment.

#### 3.2.5. Keywords and True/False/Null

PHP [keywords] MUST be in lower case.

The PHP constants `true`, `false`, and `null` MUST be in lower case.

[keywords]: http://php.net/manual/en/reserved.keywords.php

### 3.3. Namespace and Use Declarations

When present, there MUST be one blank line after the `namespace` declaration.

When present, all `use` declarations MUST go after the `namespace`
declaration.

There MUST be one `use` keyword per declaration.

There MUST be one blank line after the `use` block.

__Namespaces MUST be ordered alphabetically with a deeper namespace at the top.__

__Namespaces MAY be bundled when they share the same parent namespace of 2 levels. Bundled namespaces are separated by a empty line.__

For example:

```php
<?php

namespace ride\app;

use ride\application\Application;

use ride\library\validation\exception\ValidationException;
use ride\library\Timer;

use \Exception;

// ... additional PHP code ...
```

### 3.4. Classes, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

__An empty line goes after the declaration and before the end of the class.__

__All constants, properties and methods MUST have an empty line in between.__

#### 3.4.1. Extends and Implements

The `extends` and `implements` keywords MUST be declared on the same line as
the class name.

The opening brace for the class MUST go on __the same line as the class 
declaration__; the closing brace for the class MUST go on the next line after 
the body.

__There MUST be one space before the opening brace.__

__The class body MUST be indented once.__

~~~php
<?php

namespace Vendor\Package;

use OtherVendor\OtherPackage\BazClass;
use BarClass as Bar;
use FooClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    // constants, properties, methods
}
~~~

Lists of `implements` MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first item in the list
MUST be on the next line, and there MUST be only one interface per line.

__When the `implements` list is split across multiple lines, the opening brace 
MUST be placed on their own line.__

~~~php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable 
{
    // constants, properties, methods
}
~~~

#### 3.4.2. Properties

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

A property declaration looks like the following.

~~~php
<?php

namespace Vendor\Package;

class ClassName {

    public $foo = null;
    
}
~~~

#### 3.4.3. Methods

Visibility MUST be declared on all methods.

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on __the same line__, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

~~~php
<?php

namespace Vendor\Package;

class ClassName {

    public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
        // method body
    }

}
~~~

#### 3.4.4. Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument
list.

~~~php
<?php

namespace Vendor\Package;

class ClassName {

    public function foo($arg1, &$arg2, $arg3 = []) {
        // method body
    }

}
~~~

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

~~~php
<?php
namespace Vendor\Package;

class ClassName {

    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }

}
~~~

#### 3.4.5. `abstract`, `final`, and `static`

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

~~~php
<?php

namespace Vendor\Package;

abstract class ClassName {

    protected static $foo;

    abstract protected function zim();

    final public static function bar() {
        // method body
    }

}
~~~

#### 3.4.6. Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

~~~php
<?php

bar();

$foo->bar($arg1);

Foo::bar($arg2, $arg3);
~~~

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

~~~php
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
~~~

### 3.5. Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.

#### 3.5.1. `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

~~~php
<?php

if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
~~~

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.


#### 3.5.2. `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement MUST be indented once
from `switch`, and the `break` keyword (or other terminating keyword) MUST be
indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

~~~php
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
~~~

#### 3.5.3. `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

~~~php
<?php

while ($expr) {
    // structure body
}
~~~

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

~~~php
<?php

do {
    // structure body;
} while ($expr);
~~~

#### 3.5.4. `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

~~~php
<?php

for ($i = 0; $i < 10; $i++) {
    // for body
}
~~~

#### 3.5.5. `foreach`

A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

~~~php
<?php

foreach ($iterable as $key => $value) {
    // foreach body
}
~~~

#### 3.5.6. `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

~~~php
<?php

try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
~~~

### 3.6. Closures

Closures MUST be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

~~~php
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
~~~

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether of arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

~~~php
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
    // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
    // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};
~~~

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

~~~php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
~~~


