# M17-Regex-Tutorial-DPB

Developers write code, but they also write about code. The goal of this tutorial is to explain how a specific regular expression, or regex, functions. Below we will be selecting one regex and breaking down each part of its parts and describing their functions.

## Summary
````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Regular expressions, or regex for short, are a series of special characters that define a search pattern. In this tutorial we are trying to validate if the input is a URL

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

In regex the characters `^` and `$` are considered anchors. The caret, `^`, matches the position before the first character of the string. The, `$`, matches right after the last character of the string. 

- The string should start with either http or https then followed by ://.

### Quantifiers

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Quantifiers set the limits of the string that your regex matches (or an indivudual section of the string). URL expressions use four types of quantifiers; `+`, `?`, `{}` and `*`.

`+`: Matches the pattern one or more times. In the example regex above `([\da-z\.-]+)`, it is looking for any of the specific characters in the [] and the `+` is presents in order to match but the characters can match one or more times to be valid.
`?`: Matches the pattern zero or one time. In the example regex above `(https?:\/\/)?`, it is looking for http:// or http://. With the first `?` placed after the "s". It means the "s" is optional. Also in the example, `?`, after the https:// this means the whole first capture group is optional. It allows us to match the URL with or without the http(s)://.
`{}`: Curly brackets provide three different ways to set limites for a match. 
- `{ n }`; Matches the pattern exactly `n` number of times. 
- `{ n, }`; Matches the pattern at least `n` number of times. 
- `{ n, x }`; Matches the pattern from a minimum of `n` number of times to a maximum of `x` number of times. 
Lets look at the third capturing group, `([a-z\.]{2,6})`. The range allows for the regex to match the group of characters between two and six. This is where it is looking for .com, .net, .ca. 
`*`: Matches the pattern zero or more times. In this example we are reviewing the fourth grou `([\/\w \.-]*)*`. The expression is allow for any number of filepath characters to follow after the specific domain. Example could be https://www.google.com/images.

### OR Operator

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Using OR Operators `[]` from the regex above, `([\da-z\.-]+)`. This expression matches any characters or character classes that are between the brackets. It is looking for any digits or characters between a-z, or any "." or "-".

### Character Classes

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

A character class in a regex defines a set of characters. Any of which can occur in a input string to satisfy a match. 

`.`: Matches any character except the newling character (\n).
`\d`: Mataches any Arabic numeral digit. This cass id equivalent to the bracket expression [0-9].
`\w`: Matches any alphanumeric character from the basic Latin alphabet, including the "_". This is equivalent to the bracket expression [A-Za-z0-9_].
`\s`: Matches a single whitespace character, including tabs and line breaks


### Flags

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits of the regex. The three most common are:
`g`—Global search: the regex should be tested against all possible matches in a string.
`i`—Case-insensitive search: case should be ignored while attempting a match in a string.
`m`—Multi-line search: a multi-line input string should be treated as multiple lines.

### Grouping and Capturing

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

In the regex about we can see that there are a number of components separated by `()`. The parentheses used in regexs are to create separate groupings of intterest. 
- `(https?:\/\/)` We are interested in the https component
- `([\da-z\.-]+)\.` We are interested in the domain name (ie. www.google or www.yahoo)
- `([a-z\.]{2,6})` We are interested in the top level domain name (.com, .net, .org...)
- `([\/\w \.-]*)*` We are interested in any following filepath

### Bracket Expressions

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Anything inside a set of square brackets `[]` represents a range of characters that we are wanting to match. These patterns are known as a bracket expression but also as a positive character group. They outline the characters that we are trying to include. For example `[\da-z\.-]+`, we are looking for a string that includes any letter between a-z. If using [a-c], then we are only looking for lower case letters between a-c. 

### Greedy and Lazy Match

````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
````

Greedy matching is the defaulted(`+`, `*`) behavioral of regular expressions. The regular expression engine will try and match as much text as possible. When using `?` after another quantifier, it will because a lazy match in order to match as few of characters as possible. In a URL regex, we want to keep the quantifier greedy in or to ensure the what is being matched. 

Lets use https://www.google.com/images

In an Greedy URL regex.

Group One matches with https://. Group Two matches with www.google. Group Three matches with .com. Group Four matches with /images.

In a Lazy URL regex:

Group One matches with https://. Group Two matches with www. Group Three matches with .com/images.


### Boundaries

The metacharacter \b is an anchor like the `^` and the `$` sign. It matches at a position that is called a “word boundary”. This match is zero-length.

There are three different positions that qualify as word boundaries:

- Before the first character in the string, if the first character is a word character.
- After the last character in the string, if the last character is a word character.
- Between two characters in the string, where one is a word character and the other is not a word character.

`\b` allows you to perform a “whole words only” search using a regular expression in the form of `\bword\b`. A “word character” is a character that can be used to form words. All characters that are not “word characters” are “non-word characters”.

### Back-references

Back-references match the same text as previously matched by a capturing group. Suppose you want to match a pair of opening and closing HTML tags, and the text in between. By putting the opening tag into a backreference, we can reuse the name of the tag for the closing tag. Here’s how: <([A-Z][A-Z0-9]*)\b[^>]*>.*?</\1>. This regex contains only one pair of parentheses, which capture the string matched by [A-Z][A-Z0-9]*.

### Look-ahead and Look-behind

Sometimes it is necessary to detect merely those matches for a pattern that are preceded and followed by another pattern.

Specific syntaxes are used to meet that goal. They are known as lookahead and lookbehind. Together they are called lookaround.

As a rule, lookaround corresponds to characters, giving up the match and returning only the result: no match or match. That’s why they are considered assertions. They don’t employ characters in a string, and only state whether the match is successful or not.



## Author

I'm Dean. Looking to explore new skills and keep sharp with practice.

[My GitHub](https://github.com/Deebo18)