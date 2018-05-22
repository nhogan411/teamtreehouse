# Installing a Rails 5 Development Environment on Mac
**************************************************

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



## Introduction to Bundler
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


## Creating Static Pages in Rails

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


**************************************************
# Rails Application Walkthrough


**************************************************
# Installing a Ruby on Rails Development Environment in OS X


**************************************************
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


**************************************************
# Ruby Collections

## Ruby Arrays
Create an array in ruby via Array.new and assigning to a variable.

```
grocery_list = Array.new
```

Can also use bracket (`[]`) notation

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

An array of just strings can be built without the quotation marksusing the `%w` notation

```
grocery_list = %w(milk ggs bread)
```

Interpolating variables into an array can be done with `%W`, note the capital 'W'
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


**************************************************
# Ruby Loops
Start a loop in ruby using the `loop` keyword

```
// typically used if inside loop is more than one line of code
loop do
	// some code
end
```

or

```
// typically used if inside loop is only one line of code
loop {
	// some code
}
```

`break` keyword is used to jump out of a loop.

```
loop do
	// do a thing
	// test a thing
	if x == "the amount"
		// end the look
		break
	end
end
```


## Loop Conditionals
Create a random number by assigning `Random.new` to a variable.

We can put a limit on the random number generator with `rand(x)`

```
random_number = Random.new.rand(5) // assigns a random number between 0 and 5
```

If statements can be run on one line by switching things up a bit.

```
break if answer > 10   // executes break if answer is greater than 10
```


## The While Loop

```
answer = ""

while answer != "n"
	print "Do you want me to repeat this pointless loop again ? (y/n) "
	answer = gets.chomp.downcase
end
```

When we use the `while` loop we don't need to manually `break` the loop.

Conventional to use `i`, `j`, or `k` with loops.


## Until Loop
Opposite of the while loop in that it runs UNTIL the condition becomes true.

```
answer = "" 

until answer == "no" do
	print "Do you want this loop to continue? (y/n) "
	answer = gets.chomp
end
```


## Iteration with Each

```
array = [0, 1, 2, 3, 4, 5]

array.each do |item|  // will send each array item into the do block as variable 'item'
	puts "The current item is #{item}."
end
```

with curly braces

```
array = [0, 1, 2, 3, 4, 5]

array.each { |item|  
	puts "The current item is #{item}."
}
```

or all on one line

```
array = [0, 1, 2, 3, 4, 5]

array.each { |item| puts "The current item is #{item}." }
```

NOTE: `.each` does not affect the actual array

```
array = [0, 1, 2, 3, 4, 5]

array.each do |item|
	item = item + 2
	puts item  // prints 2, 3, 4, 5, 6, and 7 to screen 
end

puts array.inspect // original array still [0-5]
```


## Hash Iteration

```
business = { "name" => "Treehouse", "location" => "Portland, OR" }

business.each do |key, value|
	puts "the hash key is #{key} and the value is #{value}."
end
```

`.each` can also be used on hashes as `.each_pair`

Can also cycle through one specific side of the hash using `.each_key` and `.each_value`


## Times Iteration
The times iteration works on integers and will run a specific number of times.

```
// puts "hello!" 5x

5.times do 
	puts "hello!"
end
```

```
5.times do |item|
	puts "#{item}"    // outputs 0-4
end
```


## For Loops

```
for item in 1..10 do
	puts "The current item is #{item}."
end
```


## Build a Contacts list

```
contact_list = []

def ask(question, kind="string")
	print question + " "
	answer = gets.chomp
	answer = answer.to_i if kind == "number"
	return answer
end

def add_contact
	contact = {"name" => "", "phone_numbers" => []}
	contact["name"] = ask("What is the person's name?")
	answer = ""

	while answer != "n"
		answer = ask("Do you want to add a phone number? (y/n)")

		if answer == "y"
			phone = ask ("Enter a phone number:")
			contact["phone_numbers"].push(phone)
		end
	end

	return contact
end

answer = ""

while answer != "n"
	contact_list.push(add_contact())
	answer = ask("Add another? (y/n)")
end

puts "---"

contact_list.each do |contact|
	puts "Name: #{contact["name"]}"

	if contact["phone_numbers"].size > 0
		contact["phone_numbers"].each do |phone_number|
		puts "Phone: #{phone_number}"
	end

	puts "----\n"
end
```


**************************************************
# Ruby Objects and Classes
Think of classes like a blueprint that tells the class how it should be structured and what it should do.


## Instantiation

```
name = String.new("Jason")
```

In the code above, 'name' is an Instance of a 'Blueprint' String being used. Instantiation is the act of creating an instance of a class. Once an instance of a class is created it's called an object.

Classes are referred to and created in Ruby by using a capital letter and the name of the class. `String`

Objects are created using the `.new()` method. 
- `String.new`
- `Array.new`
- `Hash.new`


## Ruby Objects
`.respond_to?` method will check if an object will respond to the passed method


## Creating a Class

```
// Defines class "Name"
class Name
	def title
		"Mr."
	end

	def first_name
		"Nick"
	end

	def middle_name
		"Armen"
	end

	def last_name
		"Hogan"
	end
end

// Instantiates a new "Name" object
name = Name.new

// Displays value assigned to title in the new object name: "Mr."
puts name.title

// Displays value assigned to first_name in the new object name: "Nick"
puts name.first_name

// Displays value assigned to middle_name in the new object name: "Armen"
puts name.middle_name

// Displays value assigned to last_name in the new object name: "Hogan"
puts name.last_name
```


## Variables
In the above name class we defined my title, first, middle and last names as the values of those methods. Which is only useful if we never intend to use a different value for those methods.

Let's make this class more of a blueprint by using variables within the class.

```
// Defines class "Name"
class Name
	// Method that is run when the class is instantiated
	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	def title
		@title
	end

	def first_name
		@first_name
	end

	def middle_name
		@middle_name
	end

	def last_name
		@last_name
	end
end
```

Denote an instance variable using the `@`


## Attribrute Readers
Ruby gives us a shortcut for outputing class variables, `attr_reader`

```
// Defines class "Name"
class Name
	// Auto builds the 'title' method, so we've deleted it
	attr_reader :title
	// Auto builds the other methods, so we've deleted them
	attr_reader :first_name, :middle_name, last_name

	// Method that is run when the class is instantiated
	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end
end
```


## Attribute Writers and Accessors
In addition to `attr_reader` Ruby provides some additional shortcuts.

For instance, two ways to change a class variable:

```
// Defines class "Name"
class Name
	attr_reader :title, :first_name, :middle_name, last_name

	// Method that is run when the class is instantiated
	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	// Allows you to set new value for class variable 'title'
	def title = (new_title)
		@title = new_title
	end
end
```

The shortcut version of this new method for altering class variables is `attr_writer`

```
// Defines class "Name"
class Name
	attr_reader :title, :first_name, :middle_name, last_name
	// Allows you to set new value for class variable 'title'
	attr_writer :title

	// Method that is run when the class is instantiated
	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end
end
```

There's an even shorter method that performs the actions of both `attr_reader` and `attr_writer`: `attr_accessor`

```
// Defines class "Name"
class Name
	// Performs action of both attr_reader and attr_writer
	attr_accessor :title

	attr_reader :first_name, :middle_name, last_name

	// Method that is run when the class is instantiated
	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end
end
```


## Methods
We can create methods inside of a class, which is useful because they are only available on the instance that we are working with.

```
// Defines class "Name"
class Name
	attr_accessor :title, :first_name, :middle_name, last_name

	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	// This methods outputs the values in first, middle and last name all concatenated together
	def full_name
		@first_name + " " + @middle_name + " " + last_name
	end

	// This methods outputs the values in title, first, middle and last name all concatenated together
	def full_name_with_title
		@title + " " + full_name()
	end
end
```


## Instance Variables and Local Variables
Not every method inside of a class can see EVERY variable that we use.

A variable available to different methods in the class is an instance variable. That means the variable should be visible to the whole instance of the class.

A local variable is only available inside of the method we're working with.

This is the scope of the variable.

```
// Defines class "Name"
class Name
	attr_accessor :title, :first_name, :middle_name, last_name

	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	def full_name
		// Creates a local variable storing the first and middle names
		// This variable is ONLY available in this class
		first_and_middle_name = @first_name + " " + @middle_name

		// Uses the above variable to build the full name
		first_and_middle_name + " " + last_name
	end

	def full_name_with_title
		// Won't work because the first_and_middle_name variable is local to the full_name method
		@title + " " + first_and_middle_name + " " + @last_name
	end
end
```

We can make the first_and_middle_name varialbe available to the whole class by putting the `@` in front of it, making it an instance variable.

```
// Defines class "Name"
class Name
	attr_accessor :title, :first_name, :middle_name, last_name

	// Necessary to set the first_and_middle_name instance variable
	attr_reader :first_and_middle_name

	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	def full_name
		// Creates an instance variable storing the first and middle names
		@first_and_middle_name = @first_name + " " + @middle_name

		// Uses the above variable to build the full name
		@first_and_middle_name + " " + last_name
	end

	def full_name_with_title
		// WILL work because the @first_and_middle_name variable is available to the whole name class
		@title + " " + @first_and_middle_name + " " + @last_name
	end
end
```


## The to_s method
```
// Defines class "Name"
class Name
	attr_accessor :title, :first_name, :middle_name, last_name

	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	def full_name
		@first_name + " " + @middle_name + " " + last_name
	end

	def full_name_with_title
		@title + " " + full_name()
	end
end

name = Name.new("Mr.", "Nick", "", "Hogan")
puts name.full_name_with_title
```

`puts` is calling the `to_s` method when you call it. Instead of using a method to call `.full_name_with_title` you can call that method inside the `to_s` method to default an output.

```
// Defines class "Name"
class Name
	attr_accessor :title, :first_name, :middle_name, last_name

	def initialize(title, first_name, middle_name, last_name)
		@title = title
		@first_name = first_name
		@middle_name = middle_name
		@last_name = last_name
	end

	def full_name
		@first_name + " " + @middle_name + " " + last_name
	end

	def full_name_with_title
		@title + " " + full_name()
	end

	def to_s
		full_name_with_title()
	end
end

name = Name.new("Mr.", "Nick", "", "Hogan")
puts name    // works the same as the above code
```


## Build a Bank Account

```
class BankAccount
	attr_reader :name
	attr_accessor :transactions

	// Initializes bank account object
	// Requires a name to be passed in
	def initialize(name)
		// Set instance variable @name
		@name = name
		// Set instance array @transctions (although none created yet)
		@transactions = []
		// Set initial value of @transactions
		add_transaction("Beginning Balance", 0)
	end

	def credit(description, amount)
		add_transaction(description, amount)
	end

	def debit(description, amount)
		add_transaction(description, -amount)
	end

	def add_transaction(description, amount)
		@transactions.push(description: description, amount: amount)
	end

	def balance
		balance = 0
		@transactions.each do |transaction|
			balance += transaction[:amount]
		end
	end

	def to_s
		"name: #{name}, Balance: #{sprintf("%0.2f", balance)}"
	end

	def print_register
		puts "#{name}'s Bank Account" 
		puts "Description\tAmount

		@transactions.each do |transaction|
			puts transaction[:description] + "\t" + sprintf("%0.2f",transaction[:amount].to_s)
		end
	end
end

// Creates bank_account variable which is a BankAccount object
bank_account = BankAccount.new("Nick")
bank_account.credit("Paycheck", 100)
bank_account.debit("Groceries", 40)
```


**************************************************
# Building Web Apps with Sinatra

## Your First App
Install Sinatra

```
gem install sinatra
```

```
require "sinatra"

get("/apple/") do
	"Here's a juicy apple!"
end
```

If working in the Treehouse workspace you need to have the following right after the call to require "sinatra"

```
set :bind, "0.0.0.0"
```


## Multiple Routes in the Same App

```
get("/apple") do
  "<h1>Here's a juicy apple!</h1>"
end

get("/banana") do
  "<h1>Here's a ripe banana!</h1>"
end

get("/carrot") do
  "<h1>Here's a crunchy carrot!</h1>"
end
```


## Root Path

```
get("/") do
  "<h1>Welcome to our Wiki!</h1>"
end
```


## Getting HTML from a Template
We'll be using `.erb`  files, which stands for Embedded Ruby.

Sinatra loads the .erb files from a `/views` directory.

Add a new file to that views directory and name it `welcome.erb`

`erb :welcome` to call the welcome.erb file and display it. 


## Loading Text Files
Let's create a method to pull a .txt file and read it on the page

```
def page_content(title)
	File.read("pages/#{title}.txt")
	rescue Errno::ENOENT
	return nil
end
```

Create a new folder called `/pages`


## URL Parameters
We don't want to create a get request for EVERY page because that would turn into a huge file and wouldn't allow for dynamic pages.

Instead we'll create a kind of catch-all that grabs URL parameters

```
get "/:title" do
	params[:title]
end
```

This will grab the URL parameter like `/FirstName LastName` and spit it out to the screen.

Instead of just spitting out the `:title` parameter we will pass it into the our `page_content()` method to pull that .txt file

```
get "/:title" do
	page_content(params[:title])
end
```


## ERB Tags
Two kinds of ERB Tags, regular embedding tags and outputting embedding tags.
**Regular** - `<% %>` - ruby code goes between these open/close tags. The code is evaluated but the result doesn't get directly output. These are most frequently used to trigger loops and conditionals.

```
<% grade = 64 %>
```

This sets the grade variable to 64, but doesn't output anything.

```
<% grade = 64 %>
<% if grade > 60 %>
	// Will get output if conditional is true
	<p>Grade is passing!</p>
<% end %>
```

**Outputting** - `<%= %>` - ruby code goes between these open/close tags. The code is evaluated and gets included in the output.

```
<%= 2 + 2 %>   // outputs 4
<%= Time.now %>   // outputs current time
```

### Combining embed tags
Create a variable and cycle through each entry, outputting it to the display

```
<% [1, 5, 25].each do |number| %> 
	<p><%= number %> dollar</p>
<% end %>

// Outputs:
1 dollar
5 dollar
25 dollar
```


## Embedding Page Data with ERB
Let's use instance variables, which are available to 

```
get ":title" do
	@title = params[:title]
	@content = page_contant(@title)
	erb :show
end
```
This creates two instance variables and then calls the `show.erb` file.

We'll create that file and put some HTML inside of it that accesses our instance variables

```
<h1><%= @title %>

<p><%= @content %></p> 
```


## Saving Text Files
We've added a new method to our wiki.rb file that will take in two parameters (title and content), allowing users to create new pages.

```
def save_content(title, content)
	File.open("pages/#{title}.txt", "w") do |file|
		file.print(content)
	end
end
```

We call the `File.open` method with the name of the file we want to save our text to.

The second argument will open the file in write mode (`"w"`).


## Route Priority
Now that we've created a function or method that let's users create new files and save data to it, we need to provide a page that contains a fillable form so they can submit that data.

First things first, we need a link to the new page.

In `welcome.erb`:

```
<p>Or, you can <a href="/new">create a new page</a>.</p>
```

Now we need a route for that new page. 

In wiki.rb (before the route with the `"/:title"` the end of the file):

```
get "/new" do
	erb :new
end
```

This creates the URL location and looks at /views/new.erb for page content, so we'll need to create that now.

In the views folder create a new file called new.erb and drop in HTML to be displayed on the page when some visits /new.

```
<h1>Add New Page</h1>

<div>
	<form method="post" action="/create">
		<fieldset>
			<label id="titleLabel" for="title">Title:</label>
			<input type="text" name="title" id="title" />
		</fieldset>

		<fieldset>
			<label id="contentLabel" for="content">Content:</label>
			<textarea name="content" id="content" rows="10" columns="50"></textarea>
		</fieldset>

		<input type="submit" />
	</form>
</div>

<p><a href="/">Back to Index</a></p>
```

The HTML form is setup to send the input data to the /create page. But we don't have a page for that location, nor do we have anything in place to process the data getting passed to it, so that's what we'll take care of next.

So back at the end of the wiki.rb file we're going to setup a location for the /create page:

```
post "/create" do
	save_content(params["title"], params["content"])
	redirect "/#{params["title"]}"
end
```

We specified in our form that we're passing the URL via 'post' request, so our setup is a little different than usual. Additionally, it doesn't matter (for now) the order that we put this in the file, because it's not conflicting with an other 'get' requests.

Like parameters passed through the URL in get requests, we can utilize the parameters passed via 'post' requests using the `params` method.

Since we don't want a blank page after the user submits the form, we're going to use the `redirect` method.

All of this will work fine until we create a page that has a space in it. We're not encoding the URL in the redirect, so it gets hung up on the space.

To get around this we need to access the "uri" library that is standard with ruby.

At the top of the `wiki.rb` file

```
require "sinatra"
require "uri"
```

Then we modify the redirect path a little bit

```
redirect URI.escape("/#{params["title"]}")
```

This way, if the title of a new page has a space in it, that space is encoded into `%20` in the URL during the redirect.


## A Form to Edit an Existing Page
Similar to what we did for new pages, we need to create a link to the form to edit an existing page.

At the bottom of the show.erb page we're going to create a link to the edit page.

```
<div>
	<a href="/<%= @title %>/edit">Edit this page</a>
</div>
```

We need to know what page to edit, so we'll pass that parameter as part of the destination path for the edit page. Then we tack on "/edit" to establish that we want the edit form.

Obviously that just creates the link and doesn't actually establish a location for the page. So now we need to go to wiki.rb and establish a new location for the edit page.

```
get "/:title/edit" do
	@title = params[:title]
	@content = page_content(@title)
	erb :edit
end
```

We've established the edit page and that it'll have access to the title parameter assigned as `@title` and the content of the page (pulled using the `page_content()` method as `@content`. Now we need to create the edit page itself.

In the views folder create a new file called edit.erb. Since this form will actually be very similar to the form on new.erb, we'll use that as a template for building `edit.erb`.

```
<h1>Edit Page: <%= @title %></h1>

<div>
	<form method="post" action="/<%= @title %>">
		<input type="hidden" name="_method" value="put"> // Sinatra will recognize this hidden field and modify the request from 'post' to 'put'
		
		<fieldset>
			<label id="contentLabel" for="content">Content:</label>
			<textarea name="content" id="content" rows="10" columns="50"><%= @content %></textarea>
		</fieldset>

		<input type="submit" />
	</form>
</div>

<p><a href="/">Back to Index</a></p>
```

Important to note that we want to make this a 'put' request instead of a 'post' request. The additional notes for this page indicate that you use post for new items and put for editing items.

So now we need to create the route for the put request. In wiki.rb:

```
put "/:title" do
	save_content(params["title"], params["content"])
	redirect URI.escape("/#{params["title"]}")
end
```


## Deleting Pages
Now we need to allow for pages to be deleted.

In `wiki.rb`:

```
def delete_content(title)
	File.delete("pages/#{title}.txt")
end
```

In the `show.erb`, we're going to add a small form to delete the current page.

```
<div>
	<a href="/<%= @title =>/edit">Edit this page</a>

	<form method="post" action="<%= @title =>">
		<input type="hidden" name="_method" value="delete" />
		<input type="submit" value="Delete this page" />
	</form>
</div>
```

In `wiki.rb` we need a route for the delete method

```
delete "/:title" do
	delete_content(params["title"])
	redirect "/"
end
```


## Layouts
Instead of recreating the same HTML and CSS structure for all of our .erb files we're going to create a layout that serves as a template for site.

In the views folder create a new page called `page.erb`

```
<!DOCTYPE html>
<html>
	<head>
		<link rel="stylesheet" href="/styles.css">
	</head>

	<body>
		<%= yield %>
	</body>
</html>
```

In the `wiki.rb` file we're going to edit our erb calls to include a `layout` parameter and the file we want it to look at.

```
get "/" do
	erb :welcome, layout: :page
end

get "/new" do
	erb :new, layout: :page
end

get "/:title" do
	@title="params[:title]
	@content = page_content(@title)
	erb :show, layout: :page
end
```

But all of this is actually unnecessary.

If you only have one layout, you can set it as a default. Instead of naming your layout file `page.erb`, name it `layout.erb` and it will automatically be used in erb calls.

So change the name of `page.erb` to `layout.erb` and remove the calls from `wiki.rb`

```
get "/" do
	erb :welcome
end

get "/new" do
	erb :new
end

get "/:title" do
	@title="params[:title]
	@content = page_content(@title)
	erb :show
end
```


**************************************************
# Ruby on Rails 5 Basics
MVC - Model, View, Controller
Model - Writes Ruby objects to the database and reads them later
View - Shows data to users, most often in HTML
Controller - Respond to requests by users, cordinates with Model and View


## Creating a Rails App
`rails new blog` creates a new directory with the same name as the app, "blog"

`cd blog`
`bin/rails server` to get the rails server fired up


## Our First Resource
A Resource is a type of object that we want users to be able to:
1. **C**reate instances of
2. **R**ead data for
3. **U**pdate data for
4. **D**elete instances of
aka CRUD

Since we're creating a blog we need to create a posts resource.

### Scaffolds
Scaffolds can help setup the model, views, and controllers. Good for beginners, as you get more experienced you'll want more control and you'll set these up yourself.

```
bin/rails generate scaffold Post title:string
```
- `generate` is the sub command and will generate source code to compile for us
- `scaffold` is the type of code we want to generate
- `Post` is the model we want to make a scaffold for
- `title` is an attribute that will help describe the object we're creating
- `string` determines what type of variable the `title` should be

After the above command, we need to run a migration to create the table for posts

```
bin/rails db:migrate
```

Restart your server (`bin/rails server`) and navigate to localhost:3000/posts to see a list of posts. 

There aren't any posts yet, so click the New Post link, fill out the field to add a title (remember that's the only field we've asked for so far) and click Create Post button.

Now on the /posts page you'll see the post you've created with links to Show (read), Edit (update), and Destroy (delete).


## The Browser's Request
### How Rails Processes a Request
1. Rails looks at the request to see which code should handle it.
2. The request gets routed to an action method on that controller.
3. The controller loads the info in from the database using a model.
4. The controller generates a view using the model data


## The Controller
The controller is responsible for handling the browser request. It controls the model and the view to generate a response.

It receives the request from the URL, pulls the information from the model (typically a DB) and then presents it to the user as a view (HTML/CSS).

When we generated scaffolding for posts, the posts_controller.rb file was automatically generated in the /app/controllers folder of our application.

```
def index
	@posts = Post.all
end
```

Basically says, on page load get all Posts and assign to the local variable @posts.


## The Model
The Model is responsible for storing and retrieving data from users of the app.

Model classes are ruby classes that usually know how to read and write data from a DB.

Rails creates the code for Model classes in the /app/models sub directory.

Rails generates SQL queries for you.


## The View
The View is responsible for dispalying data to users. views usually, but not always, take the form of HTML templates, with Ruby expressions embedded in them.

Those Ruby expressions use the data from the model to populate the page with data.

Views can be found in the /app/views folder. By default the view will be /app/views/layouts/application.html.erb.

.erb files are Embedd RuBy, which is a plain text file with Ruby code embedded.

The code `<%= yield %>` is a piece of ruby code that will will actually render another template into this one.

Because we're looking at the posts page, the `yield` keyword will render in the /app/views/posts folder, specifically the indx.html.erb (because we're working with the index controller action).


## Launching Rails Console
The rails console is useful when you need to do operations on many models at once, or to look at model attributes that you haven't yet added to any views.

`bin/rails console` will start new system prompt where ruby will be evaluated (like irb)


## Rails Console: Reading Model Objects
### Read
`Post.all` will show the controller going to the model to `SELECT "posts".* FROM "posts"` and then display each of the returned posts (includes the Post id, title, created_at, and updated_at timestamps).

`Post.last` will show the controller going to the model to `SELECT "posts".* FROM "posts" ORDER BY "posts"."id" DESC LIMIT ? [["LIMIT", 1]]` and then display the single post that was returned.

`Post.find(3)` will show the controller going to the model to `SELECT "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ? [["id", 3], ["LIMIT", 1]]` and then display the single post with id=3.


## Rails Console: Creating Model Objects
`post = Post.new` will create a post variable and define it as a new instance of the Post object. By default, no values are assigned to any of the object attributes (id: nil, title:nil, etc.)

`post.title = "Hello, console!"` will assign the string to the title attribute of our post variable.

This new object won't be stored in the application database yet, so we'll need to do that ourselves.

`post.save` will show the controller going to the model and saving to the DB, `INSERT INTO "posts"("title", "created_at") VALUES (?, ?, ?) [["title", "Hello, console!"], ["created_at", 2018-01-24 11:10:00 UTC], ["updated_at", 2018-01-24 11:10:00 UTC]]`.

Now when we run `Post.all` we can see our new post is included in the results.

When we inserted our post to the database, using `post.save` an id was automatically assigned to the post.


## Rails Console: Updating Model Objects
Remeber the `post.find()` method, and that we were able to use that to pull a specific post.

By assigning the return object to a variable, we can edit the object the same we did with new objects.

`post = Post.find(3)` will pull Post object with id = 3 and assign to the post variable.

Like the new post, let's assign a new title value, `post.title = "Updated Title"` and `post.save` to save this new post title to the DB.


## Rails Console: Deleting Model Objects
`post = Post.find(4)` assigns the Post object with id = 4 to the post variable.

Now we can call the `.destroy` method on that variable to delete itm `post.destroy`

This runs an SQL query that deletes the object from the DB, `DELETE FROM "posts" WHERE "posts"."id" = ? [["id", 4]]`


## Updating the Model
We built a title into a Post object, but never added a body for the Post content. We'll need to update the Model to include that.

First we need to add a column to the database so we can store the data.
Then we need update our views to show those values.
Finally, we need to update the controller so new text can be submitted from HTML forms.

Scaffolding can't help us modify an existing resource.

```
bin/rails generate migration AddBodyToPosts body:text
```

- Anytime we want to update a DB we need to use a migration. In order to use a migration we need to use the rails `generate` command.

- The migration to create the post table was setup as part of the scaffolding earlier. Since we can't use that here, we have to build it ourselves. Instead of the `scaffold` generator, we're going to run the `migration` generator.

- The migration name comes next. Should be camel case and common format is "Add" + AttributeName  + "To" + TableName.

- Finally, specify the columns we want to add to the database with `body:text`

This command will create another file in the /db/migrate/ folder to hold the migration, BUT it's not actually performing the migration, so we still need to do that with `bin/rails db:migrate` again.

Now all Posts have a body attribute (with `nil` as default value).


## Updating Views
Now that we've added columns to the DB to store blog post content, we need to update the views on the front-end.

To do this we need to update the .erb files that render the templates.

Open up /app/views/posts/index.html.erb.
This .erb page contains a `<table>` that presents all the blog post data to viewers. We need to add a table heading (`<th>`) to the row of headings, and we need to add a field (`<td>`) in the loop that will contain some .erb code that displays the post body content (`<td><%= post.body %></td>`).

Unfortunately, this only updated the one view that displays all the posts. It doesn't edit the view of the single post. To do that, we need to edit /posts/show.html.erb.
- This page is already setup to show the post title, we just need to add a little HTML and some .erb code to display the post body. 

```
<p>
	<strong>Body: </strong>
	<%= @post.body %>
</p>
```

So now we can see the post body in the Show All view and in the Single view for the posts. But there's still spot to enter a blog post body when we edit or create new blog posts. To get that setup we need to edit the /posts/edit.html.erb and /posts/new.html.erb files. 

Unfortunately, in both of those files, there's no HTML to edit. Instead, there's a line of .erb that renders the form: `<%= render 'form', post: @post %>`. Instead of two seperate forms for managing existing and creating new posts, we actually just use the same form in both instances, this is called a partial.

### Partials
Partials are used to render pieces of a view that will get reused on multiple pages in your app. You don't want to update every page when you add a new link to the navigation. You want to update it in one place that gets reused over and over agian. This is a partial.

The partial for the Post form is at /posts/_form.html.erb
We can mimic the code for the title attribute in this file to generate some code to take in the body attribute.

```
<div class="field">
	<%= f.label :body %>
	<%= f.text_area : body %>
</div>
```


## Updating Strong Parameters
When we update a post, we're sending a POST request to the server (names unintentionally similar). A hacker could potentially hijack the POST process and send malicious data to the server. 

In order to protect against this rails has a feature called strong parameters. In every controller, you specify a list of parameters that controller will accept.

Obviously the new body attribute isn't being accepted by the controller yet.

If we head over to /app/controllers/post_controllers.rb we can see in the create method that it's calling the post_params method. In that post_params method you can see a list of permitted parameters:

```
def post_params
	params.require(:post).permit(:title)
end
```

We need to add `:body` to the list of permitted parameters.

```
def post_params
	params.require(:post).permit(:title, :body)
end
```


# Rails Routes and Resources


# Important Related Topics

# Javascript Basics

# Ruby Gems

# Troubleshooting a Rails Application