# psychic-pancake

## Regular Expression: Github Username

## Table of Contents

1. [Summary](#1-summary)
2. [Regex Basic Terminology](#2-regex-basic-terminology)
3. [Regex Pattern](#3-regex-pattern)

   3.1 [Regex Pattern Rules](#31-regex-pattern-rules)

4. [Regex Components](#regex-components)

   4.1 [Anchors](#41-anchors)

   4.2 [Quantifiers](#42-quantifiers)

   4.3 [Grouping Constructs](#43-grouping-constructs)

   4.4 [Bracket Expressions](#44-bracket-expressions)

   4.5 [Character Classes](#45-character-classes)

   4.6 [The OR Operator](#46-the-or-operator)

   4.7 [Flags](#47-flags)

   4.8 [Character Escapes](#48-character-escapes)

5. [Regex Examples](#regex-examples)

## 1. Summary

During the tenth week of my bootcamp, I was tasked with building a command line app that generated a team profile based on user input. The user would be prompted with a few questions to answer on each employee, and the final output would be in the form of an HTML webpage that displayed summaries for each team member.

The team was limited to three types of employees: manager, engineer and an intern. If the employee was an engineer, the user would have to provide the engineers Github username. It was my task to create a validation function to replicate the same functionality that would be expected from Github.

At the time of writing the code for the app, I decided on using the if-else polymorphism technique to check for invalid submissions. However, this took 14 lines of code.

```md
const gitCheck = (value) => {
if (value.length === 0) {
return 'Answer cannot be empty.';
} else if (value.indexOf(' ') >= 0) {
return 'Please delete the empty space in your answer';
} else if (value.indexOf('--') >= 0) {
return 'Cannot use consecutive hyphens in username';
} else if (value.substring(0, 1) === '-') {
return 'Cannot start with a hyphen';
} else if (value.length > 39) {
return 'Username cannot be longer than 39 characters.';
} else {
return true;
}
};
```

For this reason, I've decided to create a tutorial to explain the regex pattern that would provide the same result in less lines of code.

If you're interest in the app, please check the below link.

- Team Profile Generator Github Repo [link](https://github.com/mmehr1988/super-octo-bassoon)

While researching on how to write the regular expression for this tutorial, I came across an npm package that utilizes regular expressions for this very exact purpose. For more information, please check out the below link.

- Github Username Regex npm package [link](https://github.com/mmehr1988/super-octo-bassoon)

## 2. Regex Basic Terminology

Before jumping into the explanation of each component, I'd like to take the time to review some of the terminalogy that will be used in this tutorial.

| Term         | Definition                                                                               |
| ------------ | ---------------------------------------------------------------------------------------- |
| pattern      | A regular expression pattern is a sequence of characters that specifies a search pattern |
| string       | Text that is used to match the pattern                                                   |
| digit        | Numbers from 0-9                                                                         |
| letter       | The alphabet a-z or A-Z.                                                                 |
| symbol       | ! $ % ^ & \* ( ) \_ + \| ~ - = ` { } [ ] : ” ; ' < > ? , . /                             |
| space        | Spaces, tabs, line breaks                                                                |
| character    | A character is a letter, a digit, or symbol                                              |
| alphanumeric | A character that is either a letter or digit                                             |

## 3. Regex Pattern

```md
/^[a-z\d](<?:[a-z\d]|-(?=[a-z\d])>){0,38}$/i
```

### 3.1 Regex Pattern Rules

- Username must start and end with alphanumeric characters
- both upper and lower case characters are accepted
- Cannot include double hyphens
- Cannot include whitespace
- Max character length = 39

## 4. Regex Components

Regular expression components are characters used to build the pattern. Each character represents a specific function. In general, there are a total of eight components and we will be discussing how each have been used to build the Github Username Regex pattern.

### 4.1 Anchors

Anchors are used for position matching within a string. Typical use is for when you want to match either the beginning or the end of a string. See below summary.

| Symbol | Definition                                                                    |
| :----: | ----------------------------------------------------------------------------- |
|   ^    | The caret symbol is used for when you want to match the beginning of a string |
|   $    | The dollar symbol is used for when you want to match the end of a string      |

### 4.2 Quantifiers

Quantifiers are used for when you want to specify the number times a specific character, group, or character class should be matched within a string.

| Symbol    | Definition                   |
| --------- | ---------------------------- |
| \*        | To match zero or more times. |
| +         | To match one or more times.  |
| ?         | To match zero or one time    |
| { n }     | To match exactly n times     |
| { n , }   | To match at least n times    |
| { n , m } | To match from n to m times   |

### 4.3 Grouping Constructs

Grouping is used for when you want to apply a pattern to the substrings of an input string. As an example, "blue car" is a substring of "the blue car". To achieve this, you would use round brackets.

| Symbol | Definition                                                  |
| :----: | ----------------------------------------------------------- |
|  ( )   | Round brackets are used for when you want to create a group |

### 4.4 Bracket Expressions

A bracket expression is when you take a list of characters and place them between square brackets. The list of characters between the brackets is called a "set".

The main types of bracket expressions are either positive or negatve bracket expressions.

- Positive: When you want to match any character in the set.

- Negative: When you want to match any character not in the set.

To specify a negative expression, you simply use a caret symbol "^" at the beginning of the set.

| Symbol | Definition      | Definition                                                |
| ------ | --------------- | --------------------------------------------------------- |
| []     | Square Brackets | Square brackets are used to initiate a bracket expression |
| 123    | Character Set   | An example character set                                  |
| [123]  | Positive        | Match the digit "1" or "2" or "3"                         |
| [^123] | Negative        | Match any digit other than "1" or "2" or "3"              |

### 4.5 Character Classes

A character class is the type of character specified in the set. The character class for [123] is digits.

The below table illustrates the main types of character classes.

| Character Class Types  | Pattern       | Equivalent To | Definition                                            |
| ---------------------- | ------------- | :-----------: | ----------------------------------------------------- |
| Positive Character Set | [123]         |       -       | Match the digit "1" or "2" or "3"                     |
| Negative Character Set | [^123]        |       -       | Match any digit other than "1" or "2" or "3"          |
| Range                  | [a-e]         |       -       | Match any lower case letter from "a" to "e"           |
| digit                  | [0-9]         |      /d       | Matches any digit character                           |
| not digit              | [^0-9]        |      /D       | Matches any none digit character                      |
| white space            | [ \t\r\n\f]   |      /s       | Matches any white space                               |
| not white space        | [^ \t\r\n\f]  |      /S       | Matches any none white space                          |
| word                   | [A-Za-z0-9_]  |      /w       | Matches any alphanumeric & underscore characters      |
| not word               | [^a-za-z0-9_] |      /W       | Matches any none alphanumeric & underscore characters |

The important takeway here is the "Equivalent To" column. Think of it as shortcuts or shorthands as their known.

I'll leave it for you to decide whether it's easier to remember "/s" or "[ \t\r\n\f]" for when you want to match white spaces.

### 4.6 The OR Operator

### 4.7 Flags

### 4.8 Character Escapes

## Regex Examples

### Digits in a Phone Number

<pre>
/\d/g => +<mark>1</mark>-<mark>800</mark>-<mark>781</mark>-<mark>0342</mark>
</pre>
