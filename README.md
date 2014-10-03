php-epub-creator
================

This PHP class creates e-books using the EPUB standard format.

You can see an example inside the index.php file.

```php
<?php
ini_set('display_errors', 0);

header('Content-Type: text/html; charset=utf-8');

require 'classes/TPEpubCreator.php';

$epub = new TPEpubCreator();

// Temp folder and file name
$epub->temp_folder = 'temp_folder/';
$epub->epub_file = 'epubs/epub_name.epub';

$epub->title = 'Epub title';

// Add page from file
$epub->AddPage( false, 'file.txt', 'Título (check accent)' );

// Add pages content directly
$epub->AddPage( '<b>Test</b>', false, 'Title 2' );
$epub->AddPage( '<img src="images/2.jpg" />', false, 'Title 3' );
$epub->AddPage( '<img src="images/3.jpg" />', false, 'Title 4' );
$epub->AddPage( '<img src="images/4.jpg" />', false, 'Title 5' );

// Add image cover
$epub->AddImage( 'images/1.jpg', 'image/jpeg', true );

// Add another images
$epub->AddImage( 'images/2.jpg', 'image/jpeg', false );
$epub->AddImage( 'images/3.jpg', 'image/jpeg', false );
$epub->AddImage( 'images/4.jpg', 'image/jpeg', false );

// Create the EPUB
if ( ! $epub->error ) {
    $epub->CreateEPUB();
    
    if ( ! $epub->error ) {
        echo 'Success: Download your book <a href="' . $epub->epub_file . '">here</a>.';
    }
    
} else {
    echo $epub->error;
}
```

As simples as that!
