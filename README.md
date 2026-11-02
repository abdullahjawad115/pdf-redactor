# PDF Redactor

A browser-based tool that permanently removes sensitive text, such as names, phone numbers and email addresses, from PDF files.

It runs entirely in your browser. Your file is never uploaded anywhere.

**Try it:** https://abdullahjawad115.github.io/pdf-redactor/

## Features

- **Search for words and phrases** (one per line), plus optional built-in patterns for every email address and phone number.
- **Preview before changing anything.** Matches are highlighted on each page so you can check them first.
- **True redaction, not just black boxes.** Drawing a black box over text in a PDF doesn't remove the text underneath, so anyone can still copy it. This tool rebuilds every page that has a match as an image with the boxes burned in, so the hidden text is gone for good. Pages without matches keep their selectable text.
- **Removes hidden information** too: comments and annotations, attachments, bookmarks, and document details like title and author.
- **Checks its own work.** After building the new file, it reads it back and confirms none of your terms can still be found.
- Handles phrases split across separate pieces of text, and rotated text.

## How it works

1. **[PDF.js](https://mozilla.github.io/pdf.js/)** extracts each page's text, along with the position and size of every piece of text.
2. The pieces are joined into one string so phrases still match when the PDF has split them up. A map records which piece each character came from.
3. For each match, the tool works out a box in PDF coordinates, measuring the text to find where the match starts and ends within its piece and following the baseline for rotated text.
4. Pages with matches are rendered at 180 dpi, the boxes are painted on, and the result is placed into a brand-new PDF built with **[pdf-lib](https://pdf-lib.js.org/)**. Pages without matches are copied across with their annotations stripped.
5. The finished file is read back with PDF.js to verify that nothing matching remains.

## Use it

Open `index.html` in a modern browser, or use the live version linked above. Then:

1. Choose a PDF.
2. Type what to remove, and tick email addresses or phone numbers if you need them.
3. Click **Find matches** and check the highlights.
4. Click **Redact and download**.

## Limitations

- **Text inside images** (for example scanned pages) can't be found, because there is no text layer to search.
- Some PDFs store text without information about which characters it represents. That text can't be searched, so it won't be found or redacted.
- Redacted pages become images, so their remaining text can no longer be selected or searched.
- Always open the result and check it before sharing anything sensitive.

## Built with

JavaScript, PDF.js 3.11 and pdf-lib 1.17. Everything is in a single HTML file.

## License

MIT
