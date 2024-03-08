File signatures or magic bytes are the first few bytes of a file's content which determine their file type. For example, if a file starts with `GIF87a` or `GIF89a` which has a hex representation of `47 49 46 38 37 61` and `47 49 46 38 39 61` respectively, this indicates that it is a GIF image, while a file starting with plain text is usually considered a Text file.
> Tip #1: Alternatively, we can just have the word `GIF87a` or `GIF89a` on top of a shell, for example. `echo "GIF87a" > shell.php`. This way, we don't need to edit the bytes through hexeditor.

> Tip #2: Make sure to add "AAAA" which translates to `41 41 41 41` that way, if we want to convert our shell into a `.jpg`, the bytes that will be replaced are `41 41 41 41` and not the start of our shell.

If we changed the first bytes of any file to the GIF magic bytes, its MIME type would be changed to a GIF image, regardless of its remaining content or extension. Changing the bytes of any file can be done by tools such as [Hexedit NCurses](https://www.kali.org/tools/ncurses-hexedit/).

Web applications can also utilize this technique to determine file types, which is more accurate than just testing the file extension. The following is a example code in PHP.
```php
$type = mime_content_type($_FILES['uploadFile']['tmp_name']);

if (!in_array($type, array('image/jpg', 'image/jpeg', 'image/png', 'image/gif'))) {
    echo "Only images are allowed";
    die();
}
```