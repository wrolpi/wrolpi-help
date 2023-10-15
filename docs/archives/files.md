# Archive Files

WROLPi creates several files when archiving a webpage:

1. A [Singlefile](#singlefile) which stores an exact copy of the web page.
2. A [Readability](#readability) file.
3. A Readability text file.
4. A Readability JSON file.
5. A screenshot file of the web page.

These files are all share the same file name, but different suffixes.

| File Suffix       | Purpose                                    |
|-------------------|--------------------------------------------|
| .html             | The Singlefile.                            |
| .readability.html | The Readability extract of the Singlefile. |
| .readability.txt  | The article text extracted by Readability. |
| .readability.json | Data from Readability (URL/author/etc).    |
| .png              | The screenshot of the web page.            |

Archive files are named using three parts:

1. The domain directory
2. The archive date time (YYYY-mm-dd-HH-MM-SS).
3. The title of the web page.

If archiving [https://wrolpi.org/getting-started](https://wrolpi.org/getting-started), the resulting files would be
named like so:

```
wrolpi.org/2023-01-01-12-00-00_Getting Started.html
wrolpi.org/2023-01-01-12-00-00_Getting Started.readability.html
wrolpi.org/2023-01-01-12-00-00_Getting Started.readability.txt
wrolpi.org/2023-01-01-12-00-00_Getting Started.readability.json
wrolpi.org/2023-01-01-12-00-00_Getting Started.png
```

WROLPi will attempt to extract the Readability and create a Screenshot from the Singlefile, if this is not possible
WROLPi will still keep the lone Singlefile.
