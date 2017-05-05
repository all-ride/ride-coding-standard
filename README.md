# Ride Coding Standard

The Ride coding standard is based on the PSR standards with some changes. All changes are marked in bold to have a quick overview where this standard does not follow the PSR standards.

Read the [full specification](ride-coding-standard.md).

## PHP Code Sniffer for Ride

You can use [PHP Code Sniffer](https://pear.php.net/package/PHP_CodeSniffer/redirected) to force the Ride coding standard.
To do so, checkout this repository somewhere on your machine.

Now you can run the following command:

    phpcs --standard=/path/to/ride-coding-standard/Ride /path/to/your/SourceFile.php

To try and fix what can be fixed, replace the `phpcs` command with `phpcbf`:

    phpcbf --standard=/path/to/ride-coding-standard/Ride /path/to/your/SourceFile.php
