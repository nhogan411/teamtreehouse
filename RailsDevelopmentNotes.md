# Installing a Rails 5 Development Environment on Mac
1. Open Terminal

Rails requires several software packages. Homebrew can install these packages for us

1. Install Homebrew
 	1. Find the Homebrew website and there should be a Homebrew installation command on the page.
	2. Copy/paste that ruby command into your terminal and run it.
2. Install GPG for encryption
	1. Type into the terminal

	```
	brew install gpg
	```

Now we need to install Ruby Version Manager (RVM). This will download compile and install new ruby versions for us.

1. Install RVM
	1. Google "RVM" and probably first result
	2. Down the homepage should be a pair of commands that need to be copy/pasted into terminal
	3. Copy/paste the `gpg` command into the terminal and run it
	4. Copy/paste the `/curl` command into the terminal and run it
	5. RVM won't be available until you open a new terminal window
	
Rails is a Ruby Gem - a library or collection of reuseable code. Gems can be downloaded and installed automatically using the gems tool.

1. In terminal type `gem install` and then the name of the gem we want, `rails`, and then the particular version (skip for most recent version of rails), like `--version 5.0.0`


# Introduction to Bundler
Bundler is going to help us manage different dependencies (which Ruby Gems and whic Ruby Gem versions) for our Ruby project.

### Why do we need to manage gems/versions?
Different Gems rely on other Gems and sometimes rely on a specific version.

`gems list` in the terminal will display a list of gems and their versions. Might have more than one version installed. This is because one project might require version A and another project requites version B of the same gem. Bundler can help manage these gems and ensure you've got the right gems installed, using the `gemfile`

### Semantic Versioning
Given a version number MAJOR.MINOR.PATCH, increment the:
1. MAJOR version when you make incompatible APU changes,
2. MINOR version when you add functionality in a backwards-compatible manner, and 
3. PATCH version when you make a backwards-compatible bug fix

In Bundler, this looks like:

```
gem 'rails', '4.1.0'
```

If no version specified, the latest will be used

```
gem 'rack-cache'
```

`~>` can be used to specify versions that have the same MAJOR and MINOR version. For instance, `gem 'nokogiri', '~> 1.6.1'` means `>= 1.6.1` but `< 1.7.0`

`>=` can be used to specify ANY version greater than the speficied.

```
gem 'uglifier', '>= 1.3.0'
```

For the most part, you'll be using `bundle install`, `bundle update` and `bundle exec`

# Creating Static Pages in Rails

Let's create a new application to mess around in.

- `rails new static_pages`

Dive into the application

- `cd static_pages`

And let's make sure everything is working by running bundle

- `bundle`

Start the rails server

- `bin/rails server`

Everything is working. Cool. Stop the server for a moment.

- `control + C`
	
```
bin/rails generate controller pages --skip-assets
```

and then they kind of lost me.


# Rails Application Walkthrough


# Installing a Ruby on Rails Development Environment in OS X


# Ruby Basics
## Methods

A method is a group of code statements that perform a particular task.

`puts` or "put s" - puts a ining of charactert to the terminal output. each iing is on a new line:

```
puts(1, 2, "a", "b")

# Outputs: 
# 1
# 2
# a
# b
```

`sleep` - causes the program to pause execution for a specified number of seconds before continuing

* `sleep(2)` will set a two second pause

`print` - puts a string of characters to the terminal output. each string is on the same line

```
print("c", "d")

# Outputs:
# cd
```

Paranthesis are optional in ruby method calls
```
puts "hello world"
puts("hello world")

puts(1, 2, "a", "b")
puts 1, 2, "a", "b"

sleep(2)
sleep 2

print("c", "d")
print "c", "d"
```

## Comments
Mark text as comments using #

```
# This is a comment explaining that the new line will print "hello world"
puts "hello world"
```

## Defining Methods
Easy to define your own methods in ruby.

`def` keyword and then the name your method

```
def wait
puts "Waiting..."
sleep 3
puts "Done"
end

def count_to_three
puts 1
puts 2
puts 3
end
```

Method names:
- should be all lowercase
- should avoid having numbers in them, but it's not a rule
- should use snake case 
	- this_is_an_example_of_snake_case

To call/run a method, simply type it's name into the file

```
count-to_three
wait
```

## Variables
assign value to variables with = sign

```
number = 4
greeting = "hello"
```

to refer to the variable you simply use it

```
puts number        # outputs 4
puts greeting      # outputs "hello"
puts number + 2    # outputs 6
```

## Method Arguments
A parameter is a special variable declared at the start of a method.

```
def add(first, second)
```

In this example, first and second are both parameters or method arguments. these arguments can be used within the method body, for ptance:

```
def add(first, second)
	puts first, second
	puts first + second
end

def subtract(first, second)
	puts first, second
	puts first - second
end
```

In order to call these methods we will need to send parameter values with the call. 

```
def add(first, second)
	puts first, second
	puts first + second
end

def subtract(first, second)
	puts first, second
	puts first - second
end

add(100, 50)            # outputs value assigned to first(100) and second(50) as well as the results of the addition operation (150)

subtract(75, 25)        # outputs value assigned to first(75) and second(25) as well as the results of the subtraction operation (50)

add(3, 4)               # ooutputs value assigned to first(3) and second(4) as well as the results of the addition operation (7)

subtract(10, 5)         # outputs value assigned to first(10) and second(5) as well as the results of the subtraction operation (5)
```

## Method Return Values

```
def ask(question)
	print question
end

puts "Welcome to the widget store!"
ask "How many widgets are you ordering?"
```

`gets` waits for the user to type something and press enter and returns what the user types.

```
def ask(question)
	print question     # prints value of question to the screen
	answer = gets      # waits for the user to enter a value
	puts answer        # displays the users value to the screen
end
```

The `return` keyword in a method will send the assigned information back to the call.

```
def add(first, second)
	puts first + second
end

add(100, 50)               # outputs 150 to the screen

def addition(first, second)
	return first + second
end

puts addition(100, 50)     # outputs 150 to the screen

def sum(first, second)
	return first + second
end

result = sum(100, 50)     # assigns the result of the sum method to the result variable
```

Conveniently, the return keyword is not required to return values in a method. The last expression evaluated in that method becomes the return value.

```
def addition(first, second)
	first + second
end

puts addition(100, 50)     # outputs 150 to the screen

def sum(first, second)
	first + second
end

result = sum(100, 50)     # assigns the result of the sum method to the result variable
```

Important to remember that `return` != `puts`. `return` will return a value from a method back to the call. `puts` will print the value or whatever is passed to it.

If the last line (or `return` line) of your method is `puts` you will actually be returning a null value. 

```
def add(first, second)
	puts first + second        # prints the result of the math, but actually returns a null value
end

x = add(100, 50)               # outputs 150 to the screen but assigns NULL to variable x

def addition(first, second)
	return first + second      # simply returns the result of the math
end

y = addition(100, 50)          # no output to screen, assigns 150 to variable y
```

Back to widgets code

```
def ask(question)
	print question
	gets
end

puts "Welcome to the widget store!"
answer = ask("How many widgets are you ordering?")
puts answer
```

`answer = ask("How many widgets are you ordering?")` assigns the value of the `gets` to variable `answer`. This is outside of the method and allows us to manipulate or use the value of `answer`.

## Strings
Strings are represented with single and double quotation marks.

```
# outputs: Single-quoted strings #{represent} "Characters" verbatim.
puts 'Single-quoted strings #{represent} "Characters" verbatim.'

# outputs: Double-quoted strings make some substitutions: 6
puts "Double-quoted strings make some substitutions: #{2 + 4}"
```

## String Concatenation
`irb` in the console sets ur a testing area in the console where you can run ruby commands one at a time.

Concatenate strings using the `+` operator

```
puts "a" + "b"                      # outputs "ab"
puts "some words" + "more words"    # outputs "some wordsmore words"
puts "some words" + " " + "more words" # outputs "some words more words"
```

## String Interpolation
Interpolation can be used in double quotation markers (`"`).

Interpolation is used using interpolartion markers `#{}`

```
"aaa #{} bbb"           # outputs "aaa  bbb"
"aaa #{Time.now} bbb"   # outputs "aaa 2017-11-15 11:24:000 +000 bbb"
"a string #{1}"         # outputs "a string 1"
"a string #{1 + 2}"     # outputs "a string 3"
```

## Inspecting Values
Ruby provides a method `p` to inspect the values you pass to it, to see approximately how they'll be viewed in Ruby code.

## Escape Sequences
`\` to use escape sequences in/on strings

## Calling Methods on an Object
We're not talking about passing an argument to a method, we're talking about taking a piece of data and calling a method that's only available on that data.

```
"a string".length
"another string".upcase
"a third string.reverse

7.even?
-12.abs
5.next
```

Use `.` operator on an object to indicate we're calling a method on it.

`?` and `!` are valid characters at the end of a method name

You can string multiple methods together

```
string = "AA"  // assigns "AA" to variable "string"
string.length.even? // determines the length of string "string, and then returns true because the length is an even number
```

Only chain methods when you're certain the first method call won't fail, or you'll obviously get errors on subsequent methods.

## Classes
Methods are specific to different types of objects. You can call `.even?` on a number, but you can't call the `.length`. Similarly you can call `.length` on a string, but not `.even?`

You can get a list of methods avaialble on a given object by calling the `.methods` method.

```
p 2.methods.sort  // prints sorted list of integer methods to screen
p "AA".methods.sort  // prints sorted list of string methods to screen
```

Object class determines what methods are availalble.

Think of classes like a blueprint for building a car or radio or house. Objects are constructed using the blueprint (instances of a class). The blueprint determines the structure and what they can do, but doesn't get into the individual details of the object.

Use `.class` methods to determine the class of a given object

## Using "chomp" to Fix Our Ouput
In widget program we're taking user input, but that's including the `\n` character when the user hit `enter`. To clear that, we can use the `.chomp` method on a string to remove new line characters.

## Numeric Types
```
whole_number = 12
fractional_number = 12.34
whole_number.class  // returns Fixnum
fractional_number.class  // returns Float
```

`.even?` is a method for Fixnums, but it is not available for Floats

```
whole_number.even?  // returns an error
```

## Convert Strings to Numbers
When you ask for user input using `gets` your result is always a string, even if the user inputs a digit (1, 2, 3, etc.).

Trying to perform math on a string will cause you problems so it's important to know how to convert strings to numbers.

```
"7" * 10  // returns "7777777777", the original string repeated 10 times
"a" * 3  // returns "aaa", the original string repeated 3 times
```

`.to_i` will convert a string to an integer and `.to_f` will convert a string to a float.

## Comparison Operators
Let's create a new method that calculates the prices:

```
def price(quantity)
	quantity * 10
end
```

## "if" and "unless" Statements

```
if true
	puts "true"
	puts "additional code here"
end

if false
	puts "false"
	puts "additional code here"
end
```

```
if 75 > 50
	puts "75 > 50"  // displays on page
end

if 75 > 100
	puts "75 > 100"  // DOES NOT display on page
end

if 50 == 50
	puts "50 == 50"  // displays on page
end
```

`unless` statement runs ONLY when the result is false

```
unless 75 > 50
	puts "75 > 50"  // DOES NOT display on page
end

unless 75 > 100
	puts "75 > 100"  // display on page
end

unless 50 == 50
	puts "50 == 50"  // DOES NOT display on page
end
```

For our widgets code, come back to the price method.

```
def price(quantity)
	if quantity >= 100
		price_per_unit = 8
	elsif quantity >=50
		price_per_unit = 9
	else
		price_per_unit = 10
	end

	quantity * price_per_unit
end
```


# Ruby Collections
## Ruby Arrays
Create an array in ruby via Array.new and assigning to a variable.

```
grocery_list = Array.new
```

Can also use bracket ([]) notation

```
grocery_list = []
```

Create an array containing items by separating those items with a comma.

```
grocery_list = ["milk", "eggs", "bread"]
```

Arrays can hold objects of different classes.

```
grocery_list = ["milk", "eggs", 1, 2, 3]
```

An array of just strings can be built without the quotation marksusing the %w notation

```
grocery_list = %w(milk ggs bread)
```

Interpolating variables into an array can be done with %W, note the capital 'W'
```
item = "milk"
grocery_list = %W(#{item} eggs bread)
```

## Adding Items to Arrays
Once the array is created, there are a few ways to add items to it.

Use `.inspect` method to view the contents of an array

`<<` will append an item to an already existing array.

```
grocery_list = ["milk", "eggs", "bread"]
grocery_list << "carrots"
```

`.push` method is another option to add items to an array

```
grocery_list = ["milk", "eggs", "bread"]
grocery_list.push("potatoes")
```

`.unshift` method will add something to the begining of the array

```
grocery_list = ["milk", "eggs", "bread"]
grocery_list.unshift("celery")
```

The `+=` operator will also add items to the end of an array

```
grocery_list = ["milk", "eggs", "bread"]
grocery_list += ["ice cream", "pie"]
```

## Accessing Items in Arrays
Ruby arrays work like other languages and start the index at 0.

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list[0]  // returns "milk"
grocery_list[1]  // returns "eggs"
```

`.at` method also works

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.at(0)  // returns "milk"
grocery_list.at(1)  // returns "eggs"
```

`.first` and `.last` are quick ways to get the first and last items of the array

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.first  // returns "milk"
grocery_list.last  // returns "potatoes"
```

`-1` notation will also get you the last item in the array. this notation works backwards through the index, so it works for more than just -1 and the last item

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list[-1]  // returns "potatoes"
grocery_list[-2]  // returns "pie"
grocery_list[-3]  // returns "ice cream"
```

`.insert` method will insert a new item into the array at the specified location

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.insert(2, "oatmeal")  // puts "oatmeal at the number 2 index in the array (between "eggs" and "bread")
```

`.length` method also applies to arrays (not just strings)

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.length  // returns 6
```

`.count` method can also return the number of items in the array, but it can also be used to find out how many times an item is in the array

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.count  // returns 6
grocery_list.count("eggs")  // returns 1

grocery_list = ["eggs", "eggs", "eggs", "ice cream", "pie", "potatoes"]
grocery_list.count  // returns 6
grocery_list.count("eggs")  // returns 3
```

`.include?` method will return a boolean based on if the passed parameter is in the array

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
grocery_list.include("eggs")  // returns true
grocery_list.count("pasta")  // returns false
```

## Removing Items From Arrays
One way to remove an item from the array is to use `.pop`. This method will remove the last item (which can be assigned to a separate variable.

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
last_item = grocery_list.pop  // removes "potatoes" from grocery_list AND assigns "potatoes" to last_item variable
```

`.shift` method works the same way as .pop but on the first item in the array

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
first_item = grocery_list.shift  // removes "milk" from grocery_list AND assigns "milk" to first_item variable
```

The `.drop` method will pull a specified number of items from the end of the array for separate use. THESE ITEMS AREN'T REMOVED FROM THE ARRAY

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
drop_two_items = grocery_list.drop(2)  // assigns "pie" and "potatoes" to the drop_two_items array
```

The `.slice` method will take in a start index and a specified number of items and push to a separate array. THESE ITEMS AREN'T REMOVED FROM THE ARRAY

```
grocery_list = ["milk", "eggs", "bread", "ice cream", "pie", "potatoes"]
first_three_items = grocery_list.slice(0, 3)  // assigns "milk", "eggs", and "bread" to the first_three_items array
new_list = grocery_list.slice(2, 2)  // assigns "bread", and "ice cream" to the new_list array
```

## Ruby Hash Creation
With an Array, you can only refer to an item based on it's position or index in the array.

Inside a Hash we use an identifier to describe the item we want to access (an associative array?)

Initialize a Hash using `.new` or the `{}` notation

```
item = Hash.new
item = {}
```

To put items into a hash:
```
item = { "name" => "Bread" }
       {  KEY   =>  VALUE  }
```

To reference that item use the `[]` notation and the KEY

```
item["name"]  // returns "Bread"
```

To put multiple items in the hash

```
item = { "name" => "Bread", "quantity" => 1 }
```

Add an item using `[]` notation

```
item = { "name" => "Bread", "quantity" => 1 }
item[1] = "Grocery Store"

// returns {"name"=>"Bread", "quntity"=>1, 1=>"Grocery Store"}
```

Another way to do this is with symbols. Symbol is just like a string but with a colon in front of it. 

```
item[:name] = "Bread"
```

OR

```
item = {name: "Bread", quantity: 1}
```

`.delete` method will delete the item specified

```
item = { "name" => "Bread", "quantity" => 1 }
item.delete("name")
```

## Working with Hash Keys
Use the `.keys` method to find all the different keys associated with a hash

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.keys // returns an array of keys: ["itme", "quantity", "brand"]
```

`.has_key?` or `key?` or `.member` to test whether a specific key is available

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.has_key?("brand")  // returns true
hash.key?("brand")      // returns true
hash.member?("brand")   // returns true
```

`.fetch` method will pull the value associated with the specified key. Same as using brackets `[]`

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.fetch("quantity")  // returns 1
hash.["quantity"]       // returns 1
```

## Working with Hash Values
Similar to `.keys` we have a `.values` method that will return an array of values in the hash

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.values  // returns ["Bread", 1, "Giant Hat Bread"]
```

`.has_value?` or `.value` can be used to check if a value is in the hash

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.has_value?("Bread")  // returns true
hash.value("Bread")  // returns true
```

`.values_at` gives us the option to specify more than one key, and receive back an array of values associated with the specified keys
```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.values_at("item", "quantity")  // returns ["Bread", 1]
```

## Hash Methods
`.length` is a method that, like arrays and strings, returns the number of key/value pairs in the hash.

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
hash.length  // returns 3
```

`.invert` flips the keys and values 

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
inverted_hash = hash.invert  // same as: 
inverted_hash = {"Bread"=>"item", 1=>"quantity", "Giant Hat Bread"=>"brand"
```

`.shift` takes the first item in the hash and separates it out into a new array, removing from the original hash

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
shifted_hash = hash.shift  // returns ["item", "Bread"]
hash.inspect // returns {"quantity"=>1, "brand"=>"Giant Hat Bread"}
```

`.merge` combines two hashes, without affect either

```
hash = {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread"}
puts hash.merge({"calories"=>100}) // will display {"item"=>"Bread", "quantity"=>1, "brand"=>"Giant Hat Bread", "calories"=>100}
puts hash // still returns original hash
```

If `.merge`ing to a key that already exists you'll overwrite the old with the new

```
hash = {"item"=>"Bread"}
puts hash.merge({"item"=>"Eggs"}) // displays {"item"=>"Eggs"}
puts hash // still displays {"item"=>"Bread"}
```

## Build a Grocery List Program

```
def create_list
	print "What is the list name? "
	name = gets.chomp

	hash = { "name" => name, "items" => Array.new }
	return hash
end

list = create_list()
```

This will create a list and give it a name.

```
def add_list_item
	print "What is the item called? "
	item_name = gets.chomp

	print "How much/many? "
	quantity = gets.chomp.to_i

	hash = { "name" => item_name, "quantity" => quantity }
	return hash
end

list['items'].push(add_list_item())
```

This will ask for user to input items and quantity and add to the array associated with the items key in the first hash.

```
def print_list(list)
	puts "List: #{list['name']}"
	puts "----"

	list["items"].each do |item|
		puts "Item: " + item['name']
		puts "Quantity: " + item['quantity'].to_s
		puts "---"
	end
end

print_list(list)
```

This will clean things up the list and display a nicer looking list

```
def print_seperator(character = "-")
	puts character * 8
end

def print_list(list)
	puts "List: #{list['name']}"
	print_seperator()

	list["items"].each do |item|
		puts "\tItem: " + item['name'] + "\t\t\t" + "Quantity: " + item['quantity'].to_s
	end

	print_seperator()
end

print_list(list)
```

