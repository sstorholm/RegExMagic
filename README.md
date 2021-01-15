# RegExMagic
Useful RegEx snippets that some people might find handy

## TOC
 - [Finnish National Identitfication Numbers](#finnish-national-identitfication-numbers)
   * [Structure](#structure)
   * [RegEx - Real and Temporary IDs](#regex---real-and-temporary-ids)
   * [RegEx - Real IDs Only](#regex---real-ids-only)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Finnish National Identitfication Numbers
### Structure
Finnish National Identification Numbers (also sometimes called Social Security Numbers) have the format of `DDMMYYCZZZQ` , where `DDMMYY` is the day, month and year of birth, `C` the century sign, `ZZZ` the individual number and `Q` the control character (checksum). The sign for the century is either `+` (1800–1899), `-` (1900–1999), or `A` (2000–2099). The individual number `ZZZ` distinguishes persons with the same date of birth from each other and it is odd for males and even for females and for people born in Finland its range is 002–899. Numbers 900–999 are used for temporary personal identification, for example in hospitals, when an official ID is not known or has not yet been given to a child born.

| DD | MM | YY | C | ZZZ | Q |
|---|---|---|---|---|---|
| Day | Month | Year | Century | Individual Number | Checksum |
| 01-31 | 01-12 | 00-99 | +,- or A | 002-999 | Computed  |

The `Q` checksum is computed by taking the number `DDMMYYZZZ` and dividing it by 31, taking the remainder and then assigning a character according to the table below. 

| Remainder | Checksum Character | Comments |
|---|---|---|
| 0	| 0	|   |
| 1	| 1	|   |
| 2	| 2	|   |
| 3	| 3	|   |
| 4	| 4	|   |
| 5	| 5	|   |
| 6	| 6	|   |
| 7	| 7	|   |
| 8	| 8	|   |
| 9	| 9	|   |
| 10 | A |   |
| 11 | B |   |
| 12 | C |   |
| 13 | D |   |
| 14 | E |   |
| 15 | F |   |
| – | G	| not in use, easily confused with C |
| 16 | H |   |
| – | I	| not in use, easily confused with 1 |
| 17 | J |   |
| 18 | K |   |
| 19 | L |   |
| 20 | M |   |
| 21 | N |   |
| – | O	| not in use, easily confused with 0 |
| 22 | P |   |
| –	| Q |	not in use, reason unknown |
| 23 | R |   |
| 24 | S |   |
| 25 | T |   |
| 26 | U |   |
| 27 | V |   |
| 28 | W |   |
| 29 | X |   |
| 30 | Y |   |
| –	| Z	| not in use, easily confused with 2 |

More information (in Finnish): https://www.tuomas.salste.net/doc/tunnus/henkilotunnus.html?spm=a2c6h.14275010.0.0.7f6bdf17Psnzso#tarkm

### RegEx - Real and Temporary IDs

This RegEx matches any national identity number, both actual and temporary. 

```
(?:31|30|2\d|1\d|0[1-9])(?:12|11|10|0[1-9])(?:\d\d)[-+A]\d{3}[a-fhj-npr-yA-FHJ-NPR-Y0-9]
```

#### Features:
 - Checks that the date is real
 - Checks that the century separator is one of the allowed characters
 - Checks that the checksum character is with the correct realm, also checks for lowercase checksums incase of formatting issues. 
 
 #### Shortcomings:
 - Doesn't check that the checksum is correct
 
 ### RegEx - Real IDs Only
 
 This RegEx matches any real national identity number, but not temporary ones
 
 ```
 (?:31|30|2\d|1\d|0[1-9])(?:12|11|10|0[1-9])(?:\d\d)[-+A](?:[0-8]\d{2})[a-fhj-npr-yA-FHJ-NPR-Y0-9]
 ```
 
 #### Features:
 - Checks that the date is real
 - Checks that the century separator is one of the allowed characters
 - Checks that the checksum character is with the correct realm, also checks for lowercase checksums incase of formatting issues. 
 - Checks that the individual number is within 002 - 899
 
 #### Shortcomings:
 - Doesn't check that the checksum is correct
 

