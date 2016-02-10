# php-twig-converter

This little php script is intended to convert at best template files written 
with the PHPTemplate syntax to Twig syntax.

## Usage

You can pass directly content to the script via stdin, it will return the 
converted template through stdout.

    $ cat page.tpl.php | ./php2twig
    
You can pass file names to the script, it will create a `.tpl.twig` file at the 
same location:

    $ ls
    node.tpl.php page.tpl.php
    $ ./php2twig node.tpl.php page.tpl.php
    $ ls
    node.tpl.php node.tpl.twig page.tpl.php page.tpl.twig
    

## Options

By default when converting files, the PHPTemplate extension is `.tpl.php`, you 
can override it with `-e`:

    $ ls
    node.template
    $ ./php2twig node.template -e ".template"
    $ ls
    node.template node.tpl.twig
    

By default when converting files, the new Twig extension is `.tpl.twig`, you 
can override it with `-ne`:

    $ ls
    node.tpl.php
    $ ./php2twig node.tpl.php -ne ".html.twig"
    $ ls
    node.html.twig node.tpl.php
    

