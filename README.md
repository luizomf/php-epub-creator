# php-epub-creator

This PHP class creates e-books using the EPUB standard format.

You can see an example inside the index.php file.

```php
<?php

ini_set('display_errors', 0);
header('Content-Type: text/html; charset=utf-8');

require 'classes/TPEpubCreator.php';

$epub = new TPEpubCreator();

// Temp folder and file name
$epub->temp_folder = 'tmp/';
$epub->epub_file = 'epubs/epub_name.epub';

$epub->title = 'Epub title';

// Add page from file
$epub->AddPage(false, 'file.txt', 'Título (check accent)');

// Add pages content directly
$epub->AddPage('<b>Test</b>', false, 'Title 2');
$epub->AddPage('<img src="images/2.jpg" />', false, 'Title 3');
$epub->AddPage('<img src="images/3.jpg" />', false, 'Title 4');
$epub->AddPage('<img src="images/4.jpg" />', false, 'Title 5');

// Add cover image
$epub->AddImage('images/1.jpg', 'image/jpeg', true);

// Add other images
$epub->AddImage('images/2.jpg', 'image/jpeg', false);
$epub->AddImage('images/3.jpg', 'image/jpeg', false);
$epub->AddImage('images/4.jpg', 'image/jpeg', false);

// Create the EPUB
if (!$epub->error) {
    $epub->CreateEPUB();

    if (!$epub->error) {
        echo 'Success: Download your book <a href="' . $epub->epub_file . '">here</a>.';
    }
} else {
    echo $epub->error;
}
```

As simples as that!

## EPUB meta data

Some meta data for the EPUB can be set using the following snippets:

| Code                                                                | Effect                      |
| ------------------------------------------------------------------- | --------------------------- |
| `$epub->creator = 'Luiz Otávio Miranda';`                           | (string) Sets the creator   |
| `$epub->language = 'pt';`                                           | (string) Sets the language  |
| `$epub->rights = 'Public Domain';`                                  | (string) Sets the language  |
| `$epub->publisher = 'https://github.com/luizomf/php-epub-creator';` | (string) Sets the publisher |

## Settings

| Code                                           | Effect                                                                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `$epub->prefix_image = true;`                  | (bool) Prefixes the image names with a random number. Default: `true`.                                              |
| `$epub->delete_files_after_completion = true;` | (bool) Whether to delete all temporary fils after completion. This is a dev setting for debugging. Default: `true`. |

## Add your own CSS

You can use `$epub->css = '';` to set your own CSS for the EPUB. The entered CSS must be a string.

Example using inline CSS:

```php
$epub->css = '
    body {
        margin-right: .5em;
        margin-left: .5em;
        direction: ltr;
        font-family: "Arial", sans-serif;
        font-size: 12pt;
        font-weight: 400;
        text-align: left;
    }
';
```

Example loading a CSS file:

```php
$epub->css = file_get_contents('css/style.css', true);
```
