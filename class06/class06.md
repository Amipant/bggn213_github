# Class06
Ami Pant (A15991358)

- [Our first (silly) function](#our-first-silly-function)
- [A second function](#a-second-function)
- [A protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call our function
- Input **arguments** (there can be multiple)
- The **body**lines of R code that do the work

## Our first (silly) function

Write a function to add some numbers

``` r
add <- function(x, y = 1) {
  x + y
}
```

Now we can call this function:

``` r
add(c(10, 10), 100)
```

    [1] 110 110

``` r
add(10, 100)
```

    [1] 110

## A second function

Write a function to generate random nucleotide sequences of a user
specifies length:

The `sample()` function can be helpful here.

``` r
v <- sample(c("A", "C", "G", "T"), size = 50, replace = T)
```

I want a 1 element long character vector that looks like this “CACAGC”
not “C” “A” “C” “G” “C”

``` r
paste(v, collapse = "")
```

    [1] "TTTTACGAAGGCATGCTCCCACCTCGCCTAACCATATTTCGGCTGAGCGG"

Turn this into my first wee function

``` r
generate_dna <- function(size = 50) {
  v <- sample(c("A", "C", "G", "T"), size= size, replace = T)
  paste(v, collapse = "")
  
}
```

Test it:

``` r
generate_dna(60)
```

    [1] "CCCGTTCTAAGCGCTTAAAACCGGTTGCGACTCGCTCTCATTTCAAAACGTGCAGAGTGG"

``` r
fasta <- F
if(fasta) {
  cat("HELLO You!")
} else {
  cat("NO you dont!")
}
```

    NO you dont!

Add the ability to return a multi-element vector or a single element
fasta like vector

``` r
generate_fasta <- function(size = 50, fasta = T) {
  
v <- sample(c("A", "C", "G", "T"), size= size, replace = T)
s <- paste(v, collapse = "")

  if (fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

## A protein generating function

``` r
generate_protein <- function(size = 50, fasta = T) {
 aa  <- sample(c("A","R","N","D","C","Q","E","G","H","I",
          "L","K","M","F","P","S","T","W","Y","V"), size = size, replace = T)
 s <- paste(aa, collapse = "")

  if (fasta) {
    return(s)
  } else {
    return(aa)
  }
  
}
```

``` r
generate_protein(6)
```

    [1] "GDKCAR"

Use our new `generate_protein()` function to make random protein
sequences of length 6 to 12 (i.e. one length 6, one length 7, etc. up to
length 12)

``` r
generate_protein(6)
```

    [1] "IFHKTS"

``` r
generate_protein(7)
```

    [1] "EEREFGD"

``` r
generate_protein(8)
```

    [1] "YPFFWHQD"

``` r
generate_protein(9)
```

    [1] "SCEYTMEIM"

``` r
generate_protein(10)
```

    [1] "YGDACVGYQK"

``` r
generate_protein(11)
```

    [1] "NWQKDDWCPQM"

``` r
generate_protein(12)
```

    [1] "GPHSWEHDSTWA"

A second way is to use a `for()` loop:

``` r
lengths <- 6:12
lengths
```

    [1]  6  7  8  9 10 11 12

``` r
for (i in lengths) {
  cat(">", i, "\n", sep = "")
  aa <- generate_protein(i)
  cat(aa)
  cat("\n")
}
```

    >6
    PKYYGY
    >7
    NLTTCDA
    >8
    VFGFVVLI
    >9
    TWPPGRGGM
    >10
    RVEDFHDNCV
    >11
    EDSVLPGEYKW
    >12
    WHCHNTIGHALF

A third, and better way to solve this is to use the `apply()` family of
functions, specifically the `sapply()` function in this case.

``` r
sapply(6:12, generate_protein)
```

    [1] "FTDTHP"       "SKPDFFA"      "FSRHAHAG"     "HTTPPPWVH"    "KLPKCQNKFQ"  
    [6] "MPCGYGFRFKG"  "VKMFTAMTMTGW"
