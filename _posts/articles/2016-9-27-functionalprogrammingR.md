---
layout: post
title: Some notes on functional programming with R
---

Most of the contents here are taken fromt he R base package documents.

## **lapply {base}**

### Description

**lapply** returns a list of the same length as X, each element of which is the result of applying FUN to the corresponding element of X.

**sapply** is a user-friendly version and wrapper of lapply by default returning a vector, matrix or, if simplify = "array", an array if appropriate, by applying simplify2array(). sapply(x, f, simplify = FALSE, USE.NAMES = FALSE) is the same as lapply(x, f).  
**sapply** always return the results in a vectro if possible.  
"**s**" in **sapply** stands for "simplify". It will simplify the answer into a vector or a matrix. So if the return is a structured object, you can use lapply()

vapply is similar to sapply, but has a pre-specified type of return value, so it can be safer (and sometimes faster) to use.

replicate is a wrapper for the common use of sapply for repeated evaluation of an expression (which will usually involve random number generation).

simplify2array() is the utility called from sapply() when simplify is not false and is similarly called from mapply().

### Usage
```R
    lapply(X, FUN, ...)

    sapply(X, FUN, ..., simplify = TRUE, USE.NAMES = TRUE)

    vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)

    replicate(n, expr, simplify = "array")

    simplify2array(x, higher = TRUE)
```

### details

Simplification in sapply is only attempted if X has length greater than zero and if the return values from all elements of X are all of the same (positive) length. If the common length is one the result is a vector, and if greater than one is a matrix with a column corresponding to each element of X.

Simplification is always done in vapply. This function checks that all values of FUN are compatible with the FUN.VALUE, in that they must have the same length and type. (Types may be promoted to a higher type within the ordering logical < integer < double < complex, but not demoted.)

### value

For lapply, sapply(simplify = FALSE) and replicate(simplify = FALSE), a list.

For sapply(simplify = TRUE) and replicate(simplify = TRUE): if X has length zero or n = 0, an empty list. Otherwise an atomic vector or matrix or list of the same length as X (of length n for replicate). If simplification occurs, the output type is determined from the highest type of the return values in the hierarchy NULL < raw < logical < integer < double < complex < character < list < expression, after coercion of pairlists to lists.

vapply returns a vector or array of type matching the FUN.VALUE. If length(FUN.VALUE) == 1 a vector of the same length as X is returned, otherwise an array. If FUN.VALUE is not an array, the result is a matrix with length(FUN.VALUE) rows and length(X) columns, otherwise an array a with dim(a) == c(dim(FUN.VALUE), length(X)).

### Examples

```R
    require(stats); require(graphics)

    x <- list(a = 1:10, beta = exp(-3:3), logic = c(TRUE,FALSE,FALSE,TRUE))
    # compute the list mean for each list element
    lapply(x, mean)
    # median and quartiles for each list element
    lapply(x, quantile, probs = 1:3/4)
    sapply(x, quantile)
    i39 <- sapply(3:9, seq) # list of vectors
    sapply(i39, fivenum)
    vapply(i39, fivenum,
        c(Min. = 0, "1st Qu." = 0, Median = 0, "3rd Qu." = 0, Max. = 0))

    ## sapply(*, "array") -- artificial example
    (v <- structure(10*(5:8), names = LETTERS[1:4]))
    f2 <- function(x, y) outer(rep(x, length.out = 3), y)
    (a2 <- sapply(v, f2, y = 2*(1:5), simplify = "array"))
    a.2 <- vapply(v, f2, outer(1:3, 1:5), y = 2*(1:5))
    stopifnot(dim(a2) == c(3,5,4), all.equal(a2, a.2),
            identical(dimnames(a2), list(NULL,NULL,LETTERS[1:4])))

    hist(replicate(100, mean(rexp(10))))

    ## use of replicate() with parameters:
    foo <- function(x = 1, y = 2) c(x, y)
    # does not work: bar <- function(n, ...) replicate(n, foo(...))
    bar <- function(n, x) replicate(n, foo(x = x))
    bar(5, x = 3)
```

You can also check [this](http://stackoverflow.com/questions/3505701/r-grouping-functions-sapply-vs-lapply-vs-apply-vs-tapply-vs-by-vs-aggrega) stackoverflow page for more explanations:

> * **lapply** is a list apply which acts on a list or vector and returns a list.
> * **sapply** is a simple lapply (function defaults to returning a vector or matrix when possible)
> * **vapply** is a verified apply (allows the return object type to be prespecified)
> * **rapply** is a recursive apply for nested lists, i.e. lists within lists
> * **tapply** is a tagged apply where the tags identify the subsets
> * **apply** is generic: applies a function to a matrix's rows or columns
