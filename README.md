# RegExMagic
Useful RegEx snippets that some people might find handy

## Finnish Social Security Number / National Identitfication Number
### Structure
Finnish National Identity Numbers have the format of `DDMMYYCZZZQ` , where `DDMMYY` is the day, month and year of birth, `C` the century sign, `ZZZ` the individual number and `Q` the control character (checksum). The sign for the century is either `+` (1800–1899), `-` (1900–1999), or `A` (2000–2099). The individual number `ZZZ` distinguishes persons with the same date of birth from each other and it is odd for males and even for females and for people born in Finland its range is 002–899. Numbers 900–999 are used for temporary personal identification, for example in hospitals, when an official ID is not known or has not yet been given to a child born.

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

### RegEx

This RegEx matches any national identity number, both actual and temporary. 

#### Features:
 - Checks that the date is real
 - Checks that the century separator is one of the allowed characters
 - Checks that the checksum character is with the correct realm, also checks for lowercase checksums incase of formatting issues. 
 
 #### Shortcomings:
 - Doesn't check that the checksum is correct
 - Doesn't exclude numbers with invalid checksum characters

```
(?:31|30|2\d|1\d|0[1-9])(?:12|11|10|0[1-9])(?:[1-9]\d|0[1-9])[-+A]\d{3}[a-xA-X0-9]
```
