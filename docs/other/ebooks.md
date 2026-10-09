# eBooks

eBooks are managed by the [Docs module](../modules/docs/index.md), where they can be browsed, filtered by author and
subject, searched, and read directly in the browser with the built-in EPUB reader.

Epub files are desired as ebooks, though some support for Mobi files is provided. Reasons why WROLPi prefers Epub:

* Epub files are simple. An Epub file is a zip file containing HTML files.
* Third-party support for reading Epubs is much more feature-rich.
* Images are files in the Epub zip.
* Device support for Epubs is nearly ubiquitous.
* Because an Epub contains HTML files, it makes it easy to display them in a web browser.

EPUB eBooks and comic books open on the page you were reading; see
[Resume Where You Left Off](../system/viewing-progress.md).

Cover images are detected automatically — including Calibre-style directories with a `cover.jpg` — see
[Cover Images](../modules/docs/index.md#cover-images).

## Searching

When indexes for an eBook are generated, they are searched in the following order of precedence:

1. Title
2. Author
3. File name
4. eBook contents
