# Open Journals Publishing Artifacts

Create PDF, Crossref XML, JATS, CFF, HTML and Preprint files for an Open Journals article.

This action uses the Open Journals' Inara Docker image.

## Usage

Add a file `.github/workflows/draft-pdf.yml` to your repo.

``` yaml
on: [push]

jobs:
  paper:
    runs-on: ubuntu-latest
    name: Paper Draft
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Build draft PDF
        uses: xuanxu/publishing-artifacts@main
        with:
          journal: joss
          # This should be the path to the paper within your repo.
          paper-path: paper.md
      - name: Upload
        uses: actions/upload-artifact@v4
        with:
          name: paper
          # This is the output path where Pandoc will write the compiled
          # PDF. Note, this should be the same directory as the input
          # paper.md
          path: paper.pdf
```

This will build the paper.pdf and make it available as an artifact
after each build.

## Inputs


The build can be configured by setting the following inputs.

### `journal`

The journal for to which this paper will be submitted. May be
either `joss`, `jose` or `resciencec`. Defaults to `joss`.

### `paper-path`

Filename of the paper, relative to the project's root directory.
Defaults to `paper.md`.

### `args`

Arguments to be passed to openjournals/inara (none by default)

Options:
```
-m ARTICLE_INFO_FILE    path to the article's metadata info file

-o OUTPUT_FORMATS       output formats (html/pdf/jats/crossref/preprint/cff). Defaults to pdf & jats

-p                      Use this flag to create a production PDF without watermark and linenumbers

-r                      Meant for retraction notices that don't need to show Software/Editor/Reviewes/Submission-date information
```
