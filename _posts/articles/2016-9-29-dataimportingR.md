---
layout: post
title: Some notes on data importing with R
---

Most of the contents here are taken fromt he R base package documents.

## **read.table {utils}**

### Usage

```R
    read.table(file, header = FALSE, sep = "", quote = "\"'",
            dec = ".", numerals = c("allow.loss", "warn.loss", "no.loss"),
            row.names, col.names, as.is = !stringsAsFactors,
            na.strings = "NA", colClasses = NA, nrows = -1,
            skip = 0, check.names = TRUE, fill = !blank.lines.skip,
            strip.white = FALSE, blank.lines.skip = TRUE,
            comment.char = "#",
            allowEscapes = FALSE, flush = FALSE,
            stringsAsFactors = default.stringsAsFactors(),
            fileEncoding = "", encoding = "unknown", text, skipNul = FALSE)

    read.csv(file, header = TRUE, sep = ",", quote = "\"",
            dec = ".", fill = TRUE, comment.char = "", ...)

    read.csv2(file, header = TRUE, sep = ";", quote = "\"",
            dec = ",", fill = TRUE, comment.char = "", ...)

    read.delim(file, header = TRUE, sep = "\t", quote = "\"",
            dec = ".", fill = TRUE, comment.char = "", ...)

    read.delim2(file, header = TRUE, sep = "\t", quote = "\"",
                dec = ",", fill = TRUE, comment.char = "", ...)
```

### Details

Unless colClasses is specified, all columns are read as character columns and then converted using type.convert to logical, integer, numeric, complex or (depending on as.is) factor as appropriate. Quotes are (by default) interpreted in all fields, so a column of values like "42" will result in an integer column.

A field or line is ‘blank’ if it contains nothing (except whitespace if no separator is specified) before a comment character or the end of the field or line.

read.csv and read.csv2 are identical to read.table except for the defaults. They are intended for reading ‘comma separated value’ files (‘.csv’) or (read.csv2) the variant used in countries that use a comma as decimal point and a semicolon as field separator. Similarly, read.delim and read.delim2 are for reading delimited files, defaulting to the TAB character for the delimiter. Notice that header = TRUE and fill = TRUE in these variants, and that the comment character is disabled.


## **read_delim {readr}**

### Usage 

```R
    read_delim(file, delim, quote = "\"", escape_backslash = FALSE,
    escape_double = TRUE, col_names = TRUE, col_types = NULL,
    locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
    comment = "", trim_ws = FALSE, skip = 0, n_max = Inf,
    guess_max = min(1000, n_max), progress = interactive())

    read_csv(file, col_names = TRUE, col_types = NULL,
    locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
    comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
    guess_max = min(1000, n_max), progress = interactive())

    read_csv2(file, col_names = TRUE, col_types = NULL,
    locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
    comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
    guess_max = min(1000, n_max), progress = interactive())

    read_tsv(file, col_names = TRUE, col_types = NULL,
    locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
    comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
    guess_max = min(1000, n_max), progress = interactive())
```

### Details

Files ending in .gz, .bz2, .xz, or .zip will be automatically uncompressed. Files starting with http://, https://, ftp://, or ftps:// will be automatically downloaded. Remote gz files can also be automatically downloaded & decompressed.


## **fread {data.table}**

### Usage

```R
    fread(input, sep="auto", sep2="auto", nrows=-1L, header="auto", na.strings="NA",
    stringsAsFactors=FALSE, verbose=getOption("datatable.verbose"), autostart=1L,
    skip=0L, select=NULL, drop=NULL, colClasses=NULL,
    integer64=getOption("datatable.integer64"),         # default: "integer64"
    dec=if (sep!=".") "." else ",", col.names, 
    check.names=FALSE, encoding="unknown", strip.white=TRUE, 
    showProgress=getOption("datatable.showProgress"),   # default: TRUE
    data.table=getOption("datatable.fread.datatable")   # default: TRUE
    )
```

