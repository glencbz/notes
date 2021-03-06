
# Arrays, Hashes, Ranges & Blocks

### Objectives

- Use basic array methods including count, first, and last
- Iterate through arrays with map and each
- Use the appropriate data collection for a situation: hash vs. an object
- Get and set values for specific hash key
- Get a list of all keys in a hash

## Intro

Because you'll be using arrays & hashes so, so much in your time as a developer, we want to get you up to speed with how to work with them.

For these Ruby data collections, you'll be reminded of similar ideas in JS. That's fantastic. Anytime you can draw on that connection to help yourself guess at what methods might exist, or even just what to Google, you'll be in good shape.

## Working with Arrays

Just as a refresher – what are arrays for? What do they do? **They're for holding a collection of values**, that's it.

#### Making Arrays, Adding to Arrays

So, let's start simple – we make arrays in Ruby the same as we did in JS. Nothing unexpected here.

```ruby
numbers = [1,2,3,4]
```

Then, once you've created an array, how do you imagine you add to an array?

```ruby
numbers.push 5
# => [1,2,3,4,5]

numbers << "six"
# => [1,2,3,4,5,"six"]
```

#### Removing From Arrays

Now, obviously it's possible to mix data types (Ruby does not care), but why would we want to? That'll be weird. Let's get rid of one.

```ruby
numbers.delete "six" # give it the value you want to get rid of
# => [1,2,3,4,5]
```

#### Useful Array Miscellany

There are so many great array methods - here are a few you'll probably use from time to time.

```ruby
# how many values are there?
numbers.length # => 5, of course

# just as you'd expect, get's the value at nth index
# remember, and indexes start at 0!
numbers[3] # => 4

# a handy method equivalent to numbers[0]
numbers.first
# also a handy method equivalent to numbers[numbers.length-1]
numbers.last

# and what if we need to rearrange? so useful!
numbers = [3,2,4,1,5]
numbers.sort # [1,2,3,4,5]
numbers.sort.reverse # => [5, 4, 3, 2, 1]

# other ways to create an array
arr1 = Array.new([4,5,6])
arr2 = Array.new(3, true)
# => [true, true, true]
```

#### Mutator methods `!`
Mutator methods will not just return a value, but change the object they are called on to that value. Adding `!` to certain ruby methods will turn them into their mutator method counterparts.

*How to mutate an array*

```ruby
arr = [7,4,5]
arr.sort #not a mutator method
# => [4,5,7]
arr
# => [7,4,5]

arr = [7,4,5]
arr.sort! #the '!', aka a 'bang' will mutate the object
# => [4,5,7]
arr
# => [4,5,7]
```

#### Iterating

Now the good stuff – looping through our array and doing something with each value.

**How did we iterate over an array in JS?** It was pretty convoluted:

```js
for (var i = 0; i < numbers.length; i++) {
  console.log(numbers[i]);
};
```

We can do for loops in Ruby, too, but we've got something _much_ nicer:

```ruby
numbers.each do |number|
  puts "i am number #{number}"
end

# i am number 1
# i am number 2
# i am number 3
# i am number 4
# i am number 5
```

We can use iterators to do the same tricks we did in JS.

```ruby
foods = ['carrots', 'kale', 'beets']

# map (similar to JS map)
foods.map do |food|
  food * 2
end
# => ["carrotscarrots", "kalekale", "beetsbeets"]


# select (similar to JS filter)
foods.select do |food|
  ['carrots', 'kale'].include?(food)
end
# => ["carrots", "kale"]

# reduce (similar to JS reduce)
numbers = [1, 2, 3, 4]
numbers.reduce do |a, b|
  a + b
end
# => 10

# reduce with a starting value
numbers.reduce(10) do |a, b|
  a + b
end

# reduce applying an operation/function via a symbol
numbers.reduce(:+)
```

## Ranges

Ranges are a really powerful feature in Ruby. Used correctly, they can drastically change the way you code.

Ranges are essentially a set of values with a beginning and an end. They are enumerable, meaning you can go through their values one by one.

```ruby
a_range = (1..10) # includes 10
another_range = (1...10) # not including 10
letters_range = ('a'..'z')

# enumerables can be iterated over!
for i in (1..10) do
  puts i
end
```

You can't access individual elements with `[]` like you would with an array. However you can turn ranges into arrays.  

```ruby
another_range.to_a
=> [1,2,3,4,5,6,7,8,9]
```

We can also use the  `===`  operator to determine if an element is within a range or set

```ruby
another_range = (1...10)
another_range === 3
#=> true
another_range === 11
#=> false 
```

## Blocks

That `do`/`end` thing you're messing with is called a _block_, and it just runs the code in between, almost like a little function without a name - like anonymous functions in JavaScript or lambdas in Python.

You'll see blocks all the time, and you'll use `.each` like it's your job. It just loops through each value in your array and assigns a local variable (that you decide) to each object. You come up with what you want it called in the "pipes", aka those tall neighbors surrounding the variable: `|a_variable_of_my_choosing|`.`.each` will go through each variable and do _something_ to each variable. It's just like our `forEach` iterator in JavaScript:

```ruby
numbers = [1,2,3,4,5]

numbers.each do |number|
  puts "i am number #{number}"
end

# i am number 1
# i am number 2
# i am number 3
# i am number 4
# i am number 5
```

Oh, and for best practice, always try to name`|a_variable_of_my_choosing|` the singular tense of the array you're iterating over: ```numbers.each do |number|``` or ```articles.each do |article|```

And a bonus tip: `do`/`end` functionally is the same as `{`/`}`, so you'll see both. Use curly braces, `{ }` for single line blocks and `do ... end` for multiline blocks.
```ruby
# totally the same
numbers.each do |number|
  puts "i am number #{number}"
end

# totally the same
numbers.each {|number| puts "i am number #{number}"}
```

## Arrays - Independent Practice

Alright, practice time. Quick solo challenge, we'll be setting a timer for 10 minutes!

- Given the following list of student names, **iterate over them**, **prepending** "A+ " if their name includes an "A" in it. Make a new array if you need to
- Then, **sort the students** so that A+ students come first
- Next, **select just the students with A+** in their names. Look it up in the Ruby docs if you need to.
- Finally, **count how many A+ students you have**

```ruby
students = ['Suzy', 'Daniel', 'James', 'Mary', 'Phillip', 'Siegfried']
```

## You're Ready to Move On to Hashes - Codealong

We use hashes constantly. Hashes, like JS objects, are a great way to store related data of all different kinds, in a way that's super readable.

The key to hashes is that they always house key/value pairs. **The key describes the properties, the value is the information relating to or describing the property.**

#### Creating a Hash

To see it in action, let's pick something random in the room and try to describe it.

For example, let's describe a fan in the room.
```ruby
fan = {
  type: 'freestanding',
  blades: 5,
  speeds: ['low', 'medium', 'high'],
  rotating: false,
  height: {
    measurement: 100.4,
    unit: 'cm'
  }
}
```

Nice! Good work.

Now, based on what you know about how JS objects work, how would you guess we grab data out of here? Let's say we want to know how many blades it has.

```ruby
fan[:blades] # => 5
```

#### Symbols Are For Memory

> _"Hold up, what's the colon? In JavaScript, we'd use ``fan['blades']``, why does that not work?"_ - Roughly half the classroom, in their brains

Well, young padawans, that's because our keys up above are symbols, not strings.

Symbols are basically just like strings, except they save computer memory.  Every string you create is unique and takes up space on your computer, even if they're the same value! When we're busy looking up key/value pairs, we don't want to be wasting memory - we want it to be fast!

Let's watch:

```ruby
country = 'turkey'
food = 'turkey'

country.object_id
#=> a number

food.object_id
#=> a different number

country = :turkey
food = :turkey

country.object_id
#=> a number

food.object_id
#=> the same number!
```

Symbols on their own don't do much, but they work great as keys. There are two ways to write them:
```ruby
{
  # from older ruby versions, still totally work
  :the_old_way => 'some value',

  # from newer ruby versions, which is just shorter
  the_new_way: 'some value'
}
```

Either are fine; you'll see both a lot. Use the "new way" one if you can help it, just cuz it's nice.

For the record, strings as keys _are_ possible – we just try not to use them.

#### Adding to our hash

Real quick – what if we forgot a key/value pair, or want to add one in after the fact?

```ruby
fan[:color] = 'silver'

# {
#   type: 'freestanding',
#   blades: 5,
#   speeds: ['low', 'medium', 'high'],
#   rotating: false,
#   height: {
#     measurement: 100.4,
#     unit: 'cm'
#   },
#   color: 'silver'
# }
```

#### Guess how to get rid of a key/value pair?

Given we just learned to do this with arrays, it's okay to be unsurprised.

```ruby
fan.delete :color
# remember, parentheses are optional!
```

#### Iterating through Hashes

Iterating a hash is really easy too, we can access both the key and the value.

```ruby
car = {wheels: 4, doors: 2, seats: 5}
car.each do |key, num|
  puts "my car has #{num} #{key}"
end

# Will print out:
# my car has 4 wheels
# my car has 2 doors
# my car has 5 seats
```

## Hashes - Independent Practice

Now you try it!

- Partner up! Together and **by hand with markers on the desk**, describe your computer as a hash. Use any data types you can think of, cuz hash values can be anything!
- When you're done, each of you, independently **open your computer, write it out in IRB**. Try getting each key out, adding in new ones, and deleting ones just for fun.
- In your hashes, try to:
  - Include one key value with the value as an array
  - Include one key value with the value as another hash (look to the fan hash from earlier!)
- Remember, use the "new way" of creating hashes, if you remember how!

## Conclusion

- How do you get the 4th item of an array?
- How do you get a value out of a hash?
- How do you add a value to a hash? What about an array?
