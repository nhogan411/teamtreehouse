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
