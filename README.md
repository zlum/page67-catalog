# Page67 book catalogue

Static JSON files that the [Page67](https://github.com/zlum) Android reader downloads to show its list of
free books. Served by GitHub Pages at `https://zlum.github.io/page67-catalog/v1/`.

- `v1/index.json`: format number, build date, and per language: code, book count, file name, size.
- `v1/books-<lang>.json`: that language's books, most downloaded first, one book per line:
  `{"id":1342,"t":"Pride and Prejudice","a":"Jane Austen","n":190246,"kb":24254}`
  (Project Gutenberg ebook number, title, author, downloads in the last 30 days, EPUB size in KB).

Only text books that are public domain in the USA and have an EPUB3 file are listed. The data comes from
Project Gutenberg's offline catalogue (public domain). The app downloads a book from gutenberg.org only
when its user taps it.

## Updating (about once a month)

The generator lives in the app repository (`tools/catalog/build_catalog.py`, standard-library Python):

    curl -L -o rdf-files.tar.bz2 https://www.gutenberg.org/cache/epub/feeds/rdf-files.tar.bz2
    python ../page67/tools/catalog/build_catalog.py rdf-files.tar.bz2 .
    git add -A v1 && git commit -m "Update the catalogue" && git push

The format number in the path (`v1`) changes only when old app versions could no longer read the files.
