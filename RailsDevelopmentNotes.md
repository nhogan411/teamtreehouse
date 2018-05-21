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

