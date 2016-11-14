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

## Demo

`$ ./php2twig modules/block/block.tpl.php`

```
<div id="<?php print $block_html_id; ?>" class="<?php print $classes; ?>"<?php print $attributes; ?>>

  <?php print render($title_prefix); ?>
<?php if ($block->subject): ?>
  <h2<?php print $title_attributes; ?>><?php print $block->subject ?></h2>
<?php endif;?>
  <?php print render($title_suffix); ?>

  <div class="content"<?php print $content_attributes; ?>>
    <?php print $content ?>
  </div>
</div>
```

will convert to

```
<div id="{{ block_html_id }} " class="{{ classes }} "{{ attributes }} >

  {{ title_prefix }}
{% if block.subject %}
  <h2{{ title_attributes }} >{{ block.subject}}</h2>
{% endif %}
  {{ title_suffix }}

  <div class="content"{{ content_attributes }} >
    {{ content }}
  </div>
</div>
```



