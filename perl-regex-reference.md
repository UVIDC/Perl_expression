# Perl Regular Expression Complete Reference

This document provides a comprehensive reference for Perl regular expressions based on the official perlre documentation.

## Regular Expression Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `=~` | Bind regex to string (returns true on match) | `$string =~ /pattern/` |
| `!~` | Bind regex to string (returns true if no match) | `$string !~ /pattern/` |
| `m/pattern/flags` | Match operator | `$string =~ m/abc/i` |
| `/pattern/flags` | Match operator (shorthand) | `$string =~ /abc/i` |
| `s/pattern/replacement/flags` | Substitute operator | `$string =~ s/old/new/g` |
| `tr/searchlist/replacelist/flags` | Transliterate operator | `$string =~ tr/a-z/A-Z/` |
| `y/searchlist/replacelist/flags` | Transliterate operator (alias) | `$string =~ y/a-z/A-Z/` |
| `qr/pattern/flags` | Quote regex (compile pattern) | `my $regex = qr/pattern/i` |

## Metacharacters

| Character | Purpose | Context | Description |
|-----------|---------|---------|-------------|
| `\` | Escape the next character | Always (except when escaped by another `\`) | Makes metacharacters literal or gives special meaning to letters |
| `^` | Match beginning of string/line | Not in `[]` | Start anchor (with `/m` matches after newlines) |
| `^` | Complement character class | At beginning of `[]` | Negates character class `[^abc]` |
| `.` | Match any single character except newline | Not in `[]` | With `/s` includes newline |
| `$` | Match end of string/line | Not in `[]` | End anchor (with `/m` matches before newlines) |
| `|` | Alternation (OR) | Not in `[]` | `cat|dog` matches "cat" or "dog" |
| `()` | Grouping and capturing | Not in `[]` | Groups subpatterns and captures matches |
| `[` | Start bracketed character class | Not in `[]` | Begins character class definition |
| `]` | End bracketed character class | Only in `[]`, not first | Ends character class definition |
| `*` | Match 0 or more times | Not in `[]` | Quantifier for preceding element |
| `+` | Match 1 or more times | Not in `[]` | Quantifier for preceding element |
| `?` | Match 0 or 1 time | Not in `[]` | Quantifier for preceding element |
| `{` | Start quantifier sequence | Not in `[]` | Begins `{n,m}` quantifier |
| `}` | End quantifier sequence | Closes `{` | Ends quantifier definition |
| `-` | Character range indicator | Only in `[]` interior | Defines ranges like `a-z` |
| `#` | Comment delimiter | Only with `/x` modifier | Starts comment to end of line |

## Pattern Modifiers/Flags

### Core Modifiers

| Flag | Description | Example |
|------|-------------|---------|
| `g` | Global - match all occurrences | `/pattern/g` |
| `i` | Case-insensitive matching | `/pattern/i` |
| `m` | Multiline - `^` and `$` match line boundaries | `/pattern/m` |
| `s` | Single-line - `.` matches newline | `/pattern/s` |
| `x` | Extended - ignore whitespace and allow comments | `/pattern/x` |
| `xx` | Extended plus - ignore whitespace in character classes | `/pattern/xx` |
| `o` | Compile pattern only once (deprecated) | `/pattern/o` |
| `p` | Preserve match strings | `/pattern/p` |
| `n` | Prevent capturing in `()` groups | `/pattern/n` |

### Character Set Modifiers

| Flag | Description | Use Case |
|------|-------------|----------|
| `/a` | ASCII-safe - restrict `\d`, `\w`, `\s` to ASCII | ASCII-only matching |
| `/aa` | Strict ASCII - forbid ASCII/non-ASCII mixing | Enhanced ASCII safety |
| `/l` | Locale - use current locale rules | Locale-specific matching |
| `/u` | Unicode - use Unicode rules | Full Unicode support |
| `/d` | Default - legacy behavior (avoid) | Backward compatibility only |

### Operation-Specific Flags

| Flag | Operation | Description |
|------|-----------|-------------|
| `c` | Match | Keep position after failed match |
| `e` | Substitute | Evaluate replacement as expression |
| `ee` | Substitute | Double evaluation of replacement |
| `r` | Substitute | Non-destructive substitution |

## Quantifiers

### Standard Quantifiers

| Quantifier | Description | Equivalent | Example |
|------------|-------------|------------|---------|
| `*` | Match 0 or more times | `{0,}` | `a*` matches "", "a", "aa", "aaa" |
| `+` | Match 1 or more times | `{1,}` | `a+` matches "a", "aa", "aaa" |
| `?` | Match 0 or 1 time | `{0,1}` | `a?` matches "", "a" |
| `{n}` | Match exactly n times | - | `a{3}` matches "aaa" |
| `{n,}` | Match at least n times | - | `a{2,}` matches "aa", "aaa", "aaaa" |
| `{,n}` | Match at most n times | - | `a{,3}` matches "", "a", "aa", "aaa" |
| `{n,m}` | Match between n and m times | - | `a{2,4}` matches "aa", "aaa", "aaaa" |

### Non-Greedy Quantifiers

| Quantifier | Description | Behavior |
|------------|-------------|----------|
| `*?` | Match 0 or more times (non-greedy) | Matches minimum possible |
| `+?` | Match 1 or more times (non-greedy) | Matches minimum possible |
| `??` | Match 0 or 1 time (non-greedy) | Matches 0 if possible |
| `{n,m}?` | Match n to m times (non-greedy) | Matches minimum in range |

### Possessive Quantifiers

| Quantifier | Description | Behavior |
|------------|-------------|----------|
| `*+` | Match 0 or more times (possessive) | No backtracking |
| `++` | Match 1 or more times (possessive) | No backtracking |
| `?+` | Match 0 or 1 time (possessive) | No backtracking |
| `{n,m}+` | Match n to m times (possessive) | No backtracking |

## Escape Sequences

### Basic Escapes

| Escape | Description | Character |
|--------|-------------|-----------|
| `\t` | Tab character | Horizontal tab (HT) |
| `\n` | Newline character | Line feed (LF) |
| `\r` | Carriage return | Carriage return (CR) |
| `\f` | Form feed | Form feed (FF) |
| `\a` | Bell/alarm | Bell character (BEL) |
| `\e` | Escape character | Escape (ESC) |
| `\0` | Null character | Null byte |

### Numeric Escapes

| Escape | Description | Example |
|--------|-------------|---------|
| `\nnn` | Octal character (3 digits) | `\101` = "A" |
| `\o{...}` | Octal character (any digits) | `\o{101}` = "A" |
| `\xnn` | Hex character (2 digits) | `\x41` = "A" |
| `\x{...}` | Hex character (any digits) | `\x{41}` = "A" |
| `\N{U+nnnn}` | Unicode code point | `\N{U+0041}` = "A" |
| `\N{name}` | Named Unicode character | `\N{LATIN CAPITAL LETTER A}` |

### Control Escapes

| Escape | Description | Example |
|--------|-------------|---------|
| `\cX` | Control character | `\cA` = Ctrl-A |
| `\l` | Lowercase next character | `\lA` = "a" |
| `\u` | Uppercase next character | `\ua` = "A" |
| `\L...\E` | Lowercase until `\E` | `\Labc\E` = "abc" |
| `\U...\E` | Uppercase until `\E` | `\Uabc\E` = "ABC" |
| `\Q...\E` | Quote metacharacters until `\E` | `\Q.*\E` = literal ".*" |

## Character Classes and Special Escapes

### Predefined Character Classes

| Class | Description | ASCII Equivalent | Unicode Behavior |
|-------|-------------|------------------|------------------|
| `\d` | Decimal digit | `[0-9]` | All Unicode decimal digits |
| `\D` | Non-digit | `[^0-9]` | All non-digit characters |
| `\w` | Word character | `[A-Za-z0-9_]` | Unicode word characters + marks |
| `\W` | Non-word character | `[^A-Za-z0-9_]` | All non-word characters |
| `\s` | Whitespace character | `[ \t\n\r\f]` | All Unicode whitespace |
| `\S` | Non-whitespace | `[^ \t\n\r\f]` | All non-whitespace characters |
| `\h` | Horizontal whitespace | `[ \t]` | Unicode horizontal whitespace |
| `\H` | Non-horizontal whitespace | `[^ \t]` | All non-horizontal whitespace |
| `\v` | Vertical whitespace | `[\n\r\f]` | Unicode vertical whitespace |
| `\V` | Non-vertical whitespace | `[^\n\r\f]` | All non-vertical whitespace |
| `\R` | Any linebreak | `\r\n|\n|\r` | Unicode linebreak sequences |
| `\X` | Extended grapheme cluster | - | Unicode grapheme cluster |
| `\N` | Any character except `\n` | `[^\n]` | Not affected by `/s` |

### Bracketed Character Classes

| Pattern | Description | Example |
|---------|-------------|---------|
| `[abc]` | Match any of a, b, or c | `[aeiou]` matches vowels |
| `[^abc]` | Match anything except a, b, or c | `[^0-9]` matches non-digits |
| `[a-z]` | Match range from a to z | `[A-Za-z]` matches letters |
| `[a-zA-Z0-9]` | Match multiple ranges | Alphanumeric characters |
| `[-abc]` | Include literal hyphen (at start) | `[-+*/]` matches operators |
| `[abc-]` | Include literal hyphen (at end) | `[0-9-]` matches digits and hyphen |
| `[\]abc]` | Include literal `]` (escaped) | `[\[\]]` matches brackets |

### POSIX Character Classes

| Class | Description | ASCII Equivalent |
|-------|-------------|------------------|
| `[[:alnum:]]` | Alphanumeric characters | `[A-Za-z0-9]` |
| `[[:alpha:]]` | Alphabetic characters | `[A-Za-z]` |
| `[[:blank:]]` | Space and tab | `[ \t]` |
| `[[:cntrl:]]` | Control characters | `[\x00-\x1F\x7F]` |
| `[[:digit:]]` | Decimal digits | `[0-9]` |
| `[[:graph:]]` | Visible characters | `[!-~]` |
| `[[:lower:]]` | Lowercase letters | `[a-z]` |
| `[[:print:]]` | Printable characters | `[ -~]` |
| `[[:punct:]]` | Punctuation characters | `[!-/:-@\[-`{-~]` |
| `[[:space:]]` | Whitespace characters | `[ \t\n\r\f\v]` |
| `[[:upper:]]` | Uppercase letters | `[A-Z]` |
| `[[:xdigit:]]` | Hexadecimal digits | `[0-9A-Fa-f]` |

### Unicode Properties

| Property | Description | Example |
|----------|-------------|---------|
| `\p{Letter}` | Any letter | `\p{L}` (short form) |
| `\p{Number}` | Any number | `\p{N}` (short form) |
| `\p{Punctuation}` | Any punctuation | `\p{P}` (short form) |
| `\p{Symbol}` | Any symbol | `\p{S}` (short form) |
| `\p{Separator}` | Any separator | `\p{Z}` (short form) |
| `\p{Mark}` | Any mark | `\p{M}` (short form) |
| `\p{Other}` | Other characters | `\p{C}` (short form) |
| `\p{Script=Latin}` | Latin script characters | Language-specific |
| `\p{Block=BasicLatin}` | Unicode block | Block-specific |
| `\P{...}` | Negated property | `\P{Letter}` = non-letters |

## Assertions

### Zero-Width Assertions

| Assertion | Description | Example |
|-----------|-------------|---------|
| `^` | Start of string/line | `^The` matches "The" at start |
| `$` | End of string/line | `end$` matches "end" at end |
| `\A` | Start of string only | `\AThe` matches "The" at very start |
| `\Z` | End of string (before final `\n`) | `end\Z` matches before final newline |
| `\z` | End of string only | `end\z` matches at very end |
| `\G` | End of previous match | Continues from last match |
| `\b` | Word boundary | `\bword\b` matches whole words |
| `\B` | Non-word boundary | `\Bword\B` matches within words |
| `\K` | Keep left side out of match | `foo\Kbar` matches "bar" only |

### Advanced Boundaries

| Boundary | Description | Usage |
|----------|-------------|-------|
| `\b{wb}` | Unicode word boundary | Better than `\b` for Unicode |
| `\b{sb}` | Sentence boundary | Matches sentence breaks |
| `\b{lb}` | Line break boundary | Matches line break points |
| `\b{gcb}` | Grapheme cluster boundary | Matches grapheme boundaries |
| `\B{wb}` | Non-word boundary | Negated word boundary |

### Lookaround Assertions

| Assertion | Type | Description | Example |
|-----------|------|-------------|---------|
| `(?=...)` | Positive lookahead | Match if followed by pattern | `foo(?=bar)` matches "foo" before "bar" |
| `(?!...)` | Negative lookahead | Match if not followed by pattern | `foo(?!bar)` matches "foo" not before "bar" |
| `(?<=...)` | Positive lookbehind | Match if preceded by pattern | `(?<=foo)bar` matches "bar" after "foo" |
| `(?<!...)` | Negative lookbehind | Match if not preceded by pattern | `(?<!foo)bar` matches "bar" not after "foo" |

## Capture Groups

### Basic Groups

| Construct | Description | Behavior |
|-----------|-------------|----------|
| `(...)` | Capturing group | Captures matched text to `$1`, `$2`, etc. |
| `(?:...)` | Non-capturing group | Groups without capturing |
| `(?>...)` | Atomic/possessive group | No backtracking into group |
| `(?|...)` | Branch reset group | Resets capture numbers per branch |

### Named Groups

| Construct | Description | Access Method |
|-----------|-------------|---------------|
| `(?<name>...)` | Named capturing group | `$+{name}` or `${^CAPTURE}` |
| `(?'name'...)` | Named capturing group (alternative) | `$+{name}` |
| `(?P<name>...)` | Python-style named group | `$+{name}` |

### Backreferences

| Reference | Description | Example |
|-----------|-------------|---------|
| `\1`, `\2`, etc. | Numbered backreference | `(.).\1` matches "aba", "cdc" |
| `\g1`, `\g2`, etc. | Numbered backreference (alternative) | `(.)\g1` same as `(.)\1` |
| `\g{1}`, `\g{2}` | Numbered backreference (safer) | Avoids ambiguity |
| `\g{-1}`, `\g{-2}` | Relative backreference | `\g{-1}` refers to previous group |
| `\g{name}` | Named backreference | References named group |
| `\k<name>` | Named backreference | Alternative syntax |
| `\k'name'` | Named backreference | Alternative syntax |
| `\k{name}` | Named backreference | Alternative syntax |

### Conditional Patterns

| Pattern | Description | Example |
|---------|-------------|---------|
| `(?(1)yes|no)` | If group 1 matched | `(a)?(?(1)b|c)` matches "ab" or "c" |
| `(?(<name>)yes|no)` | If named group matched | `(?<vowel>[aeiou])?(?(vowel)x|y)` |
| `(?(condition)yes)` | If condition, match yes | `(a)?(?(1)b)` matches "ab" or "" |
| `(?(?=...)yes|no)` | If lookahead matches | Conditional based on lookahead |

### Recursive Patterns

| Pattern | Description | Usage |
|---------|-------------|-------|
| `(?R)` | Recurse entire pattern | For nested structures |
| `(?0)` | Recurse entire pattern | Alternative to `(?R)` |
| `(?1)`, `(?2)` | Recurse specific group | Recurse numbered group |
| `(?+1)`, `(?-1)` | Relative recursion | Relative group reference |
| `(?&name)` | Recurse named group | Recurse named pattern |

### Pattern Variables

| Variable | Description | Availability |
|----------|-------------|--------------|
| `$1`, `$2`, etc. | Captured group content | After successful match |
| `$+{name}` | Named capture hash | After successful match |
| `$&` | Entire matched string | After successful match |
| `$`` | String before match | After successful match |
| `$'` | String after match | After successful match |
| `$+` | Last matched group | After successful match |
| `$^N` | Most recently closed group | During match |
| `${^PREMATCH}` | String before match | With `/p` flag |
| `${^MATCH}` | Entire matched string | With `/p` flag |
| `${^POSTMATCH}` | String after match | With `/p` flag |

## Extended Patterns

### Comments and Documentation

| Pattern | Description | Usage |
|---------|-------------|-------|
| `(?#...)` | Embedded comment | `(?# This is a comment)` |
| `# comment` | Line comment | Only with `/x` flag |

### Code Evaluation (Perl-Specific)

| Pattern | Description | Usage |
|---------|-------------|-------|
| `(?{code})` | Execute Perl code | `(?{$count++})` |
| `(??{code})` | Dynamic pattern | `(??{$dynamic_pattern})` |
| `(?(?{code})yes|no)` | Conditional code | Execute code for condition |

### Pattern Modifiers Within Regex

| Modifier | Description | Example |
|----------|-------------|---------|
| `(?i)` | Case insensitive on | `(?i)abc` matches "ABC" |
| `(?-i)` | Case insensitive off | `(?-i)abc` matches "abc" only |
| `(?x)` | Extended syntax on | Ignore whitespace |
| `(?s)` | Single line on | `.` matches newline |
| `(?m)` | Multiline on | `^` and `$` match line boundaries |
| `(?adlup)` | Character set modifiers | Various character set rules |

---

*This reference is based on the official Perl documentation (perlre). For the most current information, consult `perldoc perlre` or visit [https://perldoc.perl.org/perlre](https://perldoc.perl.org/perlre).*