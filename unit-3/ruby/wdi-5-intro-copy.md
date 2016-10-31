### Input / Output

You've already seen how `puts` will output information to the screen. What if we want to accept user input? Let's try `gets`.

```ruby
puts "Enter your name:"
you = gets

puts "Enter a friend's name:"
friend = gets

puts "Hello, #{friend}. #{you} says hi."

# Outputs
# Enter your name:
# Tim
# Enter a friend's name:
# Bob
# Hello, Bob
# . Tim
#  says hi.
```

That almost works as we want, but `gets` is reading in the newline
character from when we pressed the Enter key. Generally, when reading user input we want to `chomp` the data. (See http://www.ruby-doc.org/docs/Tutorial/part_02/user_input.html)

```ruby
puts "Enter your name:"
you = gets.chomp

puts "Enter a friend's name:"
friend = gets.chomp

puts "Hello, #{friend}. #{you} says hi."

# Enter your name:
# Tim
# Enter a friend's name:
# Frank
# Hello, Frank. Tim says hi.
```

Much better. Now the unnecessary newlines are removed, thanks to `chomp`.
