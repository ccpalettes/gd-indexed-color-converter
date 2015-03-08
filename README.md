GDIndexedColorConverter
=======================

[GDIndexedColorConverter](https://github.com/ccpalettes/gd-indexed-color-converter) is a
simple library that convert an image into [indexed color](http://en.wikipedia.org/wiki/Indexed_color)
mode. With indexed color mode, an image can be displayed with only a few specific colors.

To archieve image dithering effect, GDIndexedColorConverter uses [Floyd–Steinberg dithering]
(http://en.wikipedia.org/wiki/Floyd%E2%80%93Steinberg_dithering) algorithm to apply error
diffusion of each pixel onto its neighboring pixels.

Requirements
------------

Since GDIndexedColorConverter uses some functions of the
[GD extension](http://php.net/manual/en/book.image.php), you need to the enable GD extension
in the PHP configuration file ([`php.ini`](http://php.net/manual/en/ini.php)).

Usage
-----

GDIndexedColorConverter provide a function named `convertToIndexedColor` to convert an image
into indexed color mode, it accepts three parameters(listed below), and return a new image
resource of indexed color mode.

- `im` *(imageresource)* The image resource created by the functions of GD library.

- `palette` *(array)* The palette which contains all the specific colors that the indexed-color-mode
image will use. This parameter is an array which stores all the colors, each color is an
indexed array that consists of red, green and blue color channel values.

- `dither` *(float)* How much the Floyd–Steinberg dithering algorithm will affect the
image. This parameter is optional, its default value is 0.75, and the value must be between
0 and 1.

**Code example:**

```php
	// create an image
	$image = imagecreatefromjpeg('example.jpg');

	// create a gd indexed color converter
	$converter = new GDIndexedColorConverter();

	// the color palette
	$palette = array(
		array(0, 0, 0),
		array(255, 255, 255),
		array(255, 0, 0),
		array(0, 255, 0),
		array(0, 0, 255)
	);

	// convert the image to indexed color mode
	$new_image = $converter->convertToIndexedColor($image, $palette, 0.8);

	// save the new image
	imagepng($new_image, 'example_indexed_color.png', 0);
```

Dithers
-------

Applying different dither values on indexed-color images, you can get various image effects.
In the `example` folder, there is a simple example that creates three indexed images with
different dither values(0.2, 0.4, 0.8) and five colors(white, black, red, green and blue).

![Example Output](https://raw.githubusercontent.com/ccpalettes/gd-indexed-color-converter/gh-pages/storage/example_output.jpg)

The example image [`shell.jpg`](https://www.flickr.com/photos/sagesolar/10894165595) is
created by [@sage_solar](https://www.flickr.com/photos/sagesolar/). The image is under
[Creative Commons License](https://creativecommons.org/licenses/by/2.0/).

License
-------
GDIndexedColorConverter is licensed under the [MIT license]
(https://raw.githubusercontent.com/ccpalettes/gd-indexed-color-converter/master/LICENSE).

Copyright (c) 2014 [Jeremy Yu](https://github.com/ccpalettes) <ccpalettes@gmail.com>

