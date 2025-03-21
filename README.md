# Slang v0.1.0
*by Ren Softworks*

**Slang** stands for ***Straightforward Language for Godot***. The following names are also appropriate:
- Simple Language
- Stupid Language for Grumpy People
- Sh\*tty Language that is Godawful

Slang is a readable, editor-friendly configuration language meant primarily to store objects as collections of key-value pairs. Slang documents can be mapped to a hash table or dictionary in any other language (but I wrote it specifically for Godot). 

Slang was written primarily for these reasons:
- While Godot comes with JSON support out-of-the-box, the lack of comments and strict syntax requirements make it cumbersome to work with at scale.
- Godot 4.x lacks support of alternatives like YAML and TOML, and the project appears to be dragging its feet when it comes to correcting this.
- Godot's ConfigFiles aren't enough to support the requirements for my current project.
- This project started as an attempt to implement TOML in GDScript, but then I realized that inline tables in TOML kind of suck and I wasn't going to have it.
- I don't have the time or motivation to write a YAML implementation.
# Objectives

- **Minimalist** - Slang supports a minimal number of base value types. It expects you to construct more complex types of data from these base types (such as through nested tables), or you can have your application's code do all the heavy lifting. Consequently, the Slang spec aims to be as short and concise as possible and should be relatively simple to implement.
- **Editor-friendly** - A human should be able to reasonably read a well-formatted Slang document and edit it. Additionally, it should be easy to compose brand-new Slang documents from scratch.
# Spec

Slang documents should use the extension `.slang`. If you want the document to show up in the Godot editor, `.slang.cfg` also works. Really, just do whatever you want. It's your app, not mine.
## Comments

Comments are preceded by a hash symbol and terminated by a newline.

```
# This is a comment.
my_key = "my_value" # This is a comment at the end of a line.
```
## Separators

Separators are considered to be any whitespace character (including newline) and the comma `,`. Generally, these characters are ignored outside of arrays and tables. Place them anywhere you think they could enhance (or hinder) readability.

```
# Kind of ugly
my_key = value my_other_key = my_other_value

# Better
my_key = value, my_other_key = my_other_value

# Even better
my_key = value, 
my_other_key = my_other_value

# Are you okay?
my_key,,,,,,,,,,         ,,            =,
,,,,,,,,,,"value" my_other_key=my_other_value
```
## Key/Value Pairs

The entirety of a Slang document is made up of key/value pairs. Separators between the key, equals sign, and value are ignored. Keys can be words, strings, or numbers. Values can be any data type.

```
# This is a valid key/value pair.
key = value

# These are also valid.
"key" = "value"
679 = value

# Also valid.
key
=
value
```
## Words

Words are any characters that are strung together without quotes, excluding separator characters and other functional characters explained in this spec. 

```
my_word                 # This is a word.
my_word my_other_word   # These are two words.
my_word,my_other_word   # These are also two words.
```

Words typically parse into strings when used as keys and values. Certain words, like `null`, `true`, or `false` can be parsed into their own types when used as a value depending on the parser's language, but otherwise have no special meaning in Slang.
## Strings

Strings are any collection of characters strung together and enclosed by double quotes `"`. Double quotes can be escaped by a preceding backslash `\`.

```
my_string = "I'm a string!"
quote = "\"Schlong\" was flabbergasted to hear about the grisly events of 1999"
```
## Numbers

Numbers are any numeric characters that are strung together, with or without a decimal point. Slang does not distinguish between integers or floating-point numbers. Numbers should typically be parsed as floats.

```
my_integer = 12345  # A number.
pi = 3.14159        # A decimal number.
negative = -0.69    # A negative number.
```
## Arrays

Arrays are a collection of values enclosed in square brackets `[]`. Separators must exist between each value in the array.

```
fruits = ["apples", "oranges", "bananas"]
lucky_numbers = [72 7 12]
nested_array = [
	[1,2,3]
	[4,5,6]
]
```
## Tables

Tables are a collection of key/value pairs enclosed in curly braces `{}`. Separators must exist between each key/value pair.

```
my_things = {
	my_key = value
	my_lie = true
	my_lucky_numbers = [72, 7, 12]
	my_info = {
		name = "John Smith",
		age = 7,
		email = "jsmith@example.com"
	}
}
```
