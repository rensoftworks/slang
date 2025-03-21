# Slang for GDScript

It's exactly what the title says. I've been using it for a few weeks now to store data for my current project. Nothing's exploded yet, so I think it's worth publishing.

## Usage

Just drop slang.gd somewhere in your project.

```
# Parse a Slang document as a string
Slang.parse(my_string)

# Convert a dictionary into a Slang document
Slang.stringify(my_dictionary)
```

## Caveats

This thing is noticeably slower than Godot's native JSON implementation, especially with large documents. As of this writing I can't tell whether that's my fault as a programmer, a limitation with GDScript, or something else. You can always convert your Slang documents to JSON if this becomes an issue.
