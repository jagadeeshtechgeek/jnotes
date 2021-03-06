# regex

RegEx:

## Meta Characters:

* Position
* Single Character
* Quantifiers
* Character Classes
* Alternation
* Capturing Groups 
* Capturing Back Reference

### Position Boundaries

^ Matches beginning of input $ Matches end of input \b Matches a word boudry

### Single Character:

\d Matches any digit or \[0-9\] \w Matches any alphanumeric character and underscore \[A-Za-z0-9\_\] \s Matches any white space \(including space, tab, form feed, line feed\) . Matches any character whatsoever

### Quantifiers:

x\* Matches the preceding item x \(0 or more times\) x+ Matches the preceding item x \(1 or more times\) x? Matches the preceding item x \(0 or 1 time\) \(used for Optional char check\) \ colou?rs? x{min, max} Matches values between min and max quantities \ \d{3,5} x{n} Matches 'n' times \ \d{3}

### Character Classes:

\[abcdef\] Matches a or b or c or d or e or f \[a-f\] Matches a or b or c or d or e or f \[a-z\] Matches a or b or c or .... or z \[A-Z\] Matches A or B or C or .... or Z \[0-9\] Matches 0 or 1 or 2 or 3 .... or 9

\[a-zA-Z\] Matches 'A to Z' or 'a to z' \[0-9a-zA-Z\] Matches '0 to 9' or 'A to Z' or 'a to z'

\[-.\] Matches - or . \[-. ,\] Matches - or . or space or ,

\[abc\] Matches a or b or c \[abc\(\] Matches a or b or c or '\(' // why '\(' instead of just '\(' ? // '\(' used in Alternation

 Matches any thing not 'a or b or c' \[a^bc\] Matches a or ^ or b or c \[\^abc\] Matches ^ or a or b or c

### Alternation:

\(com\|net\|org\) Matches 'com' or 'net' or 'org' .\(com\|net\|org\) Matches '.com' or '.net' or '.org'

### Capturing Groups:

\(x\) Matches x and remembers the match

### Capturing Back Reference:

\n A back reference to the last substring matching the n parenthetical in the regular expression \(counting left parentheses\).

### Examples \(Single Character & Quantifiers\):

#### \d\d\d

```text
123     //matches '123'
408     //matches '408'
1234    //matches '123'
1a23    // no match
1a234   // matches '234'
```

#### \d{3}

```text
123     //matches '123'
408     //matches '408'
1234    //matches '123'
```

#### \d{3,5}     //min:3 max:5 digits

```text
123     //matches '123'
408     //matches '408'
12345    //matches '12345'
123456    //matches '12345'
```

### Examples \(Position\):

#### ^\w+

```text
hi hello    // matches 'hi'
hi          // matches 'hi'
hello       // matches 'hello'
```

#### \w+$

```text
hi hello
// matches 'hello'

hi
// matches 'hi'

hello
// matches 'hello'
```

#### ^\w+$

```text
hi hello
// no match

hi
// matches 'hi'

hello
// matches 'hello'
```

#### \b\w+\b

```text
hi hello
// matches 'hi' and 'hello'

hi
// matches 'hi'

hello
// matches 'hello'

408.533.5628
// matches '408' and '533' and '5628'
```

### Examples \(Character Classes\):

```text
\(?\d{3}\)?[-. ]\d{3}[-. ]\d{4}

408-533-5628

408 533 5628

408.533.5628

(408) 533 5628
```

### Examples \(Character Classes & Alternation\):

```text
@gmail.com
jagadeeshthegeek@gmail.com
jagadeesh.the.geek@gmail.org



[\w.]*@\w+\.(com|net|org)
// matches: '@gmail.com'
// matches: jagadeeshthegeek@gmail.com
// matches: jagadeesh.the.geek@gmail.org


[\w.]+@\w+\.(com|net|org)


// matches: jagadeeshthegeek@gmail.com
// matches: jagadeesh.the.geek@gmail.org

// Does Not Matches: @gmail.com  // need 1 or more  --before @
```

#### Greedy Match & Not Greedy Match:

```text
    . matches any char
    * any number
    .* matches any char any number (Greedy Match)
    .*? matches any char any number (Not Greedy Match)
```

Greedy Match:

```text
\[.*\]
[My Link1] anytextanytextanytext [My Link2]

// matches everything '[My Link1] anytextanytextanytext [My Link2]'
```

Not Greedy Match:

```text
\[.*?\]      

[My Link1] anytextanytextanytext [My Link2]

// matches '[My Link1]'
// matches '[My Link1]'
```

### Examples \(Capturing Groups\) & Replace:

```text
    Regex               --->    Replace
(\d{3})-\d{3}-\d{4}     --->    $1-XXX-XXXX

408-533-5628            --->    408-XXX-XXXX
901-533-5628            --->    901-XXX-XXXX
```

```text
\[(.*?)\]\((.*?)\)      --->    <a href="$2"> $1 </a>

[My Link1](http://mylink1.com)  --->    <a href="http://mylink1.com"> My Link1 </a>
[My Link2](http://mylink2.com)  --->    <a href="http://mylink2.com"> My Link2 </a>
```

### Examples \(Capturing Back Reference\):  \(group1\)  --&gt;  use it as \1

```text
\b(\w+)\s\1\b
```

this is double double match //matches 'double double' this is sameword sameword match //matches 'sameword sameword' this does not match not

