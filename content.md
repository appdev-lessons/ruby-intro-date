# The Date class

Sure, we could just use a `String` to represent a date, like `"April 19, 1987"`. But Ruby has a built-in class that makes it much easier to work with dates: `Date`.

## Creating a date

The `Date` class isn't loaded into every Ruby program by default, so to use it we first need to say

```ruby
require "date"
```

(Usually we omit the parentheses around the string argument to the `require` method. Just like when we use `pp "Hello, world!"` as opposed to `pp("Hello, World!")`.)

### Date.new

After `require "date"`, we can create a new instance as usual with `.new`:

```ruby
new_date = Date.new
pp new_date
pp new_date.class
```
{: .repl #new_date title="Date.new" points="1"}

Did that work? Or did you get an error message? Maybe add the `require "date"` statement before you call the `Date` class!

By default, the new date is January 1st, of the year −4712! Interesting, but not very helpful.

<aside markdown="1">
Year 1 of the [Julian Period](https://en.wikipedia.org/wiki/Julian_day) was 4713 BC (−4712).
</aside>

You can also pass `Date.new` arguments to initialize with a specific year, month, and day:

```ruby
require "date"

pp Date.new(2001)

pp Date.new(2001,2,3)

# a negative day?! we can count backwards 
# (more on that soon)
pp Date.new(2001,2,-1)
```
{: .repl #new_date_args title="Date.new with arguments" points="1"}

## Date Methods

### Date.today 

The `Date.today` method returns an object initialized to the current date.

```ruby
require "date"
pp Date.today
```
{: .repl #date_today title="Date.today" points="1"}

### year 

Call the `year` method on a `Date` object to return just the year of the date as an `Integer`.

```ruby
require "date"
t = Date.today
pp t.year
```
{: .repl #date_year title="Date.today.year" points="1"}

- What would you type after `t.year` above to convert the variable to a `String`?
- .to_s
    - Yes! That's the method we need.
{: .free_text #to_string title="Integer to String" points="1" answer="1" }

### month 

Call the `month` method on a `Date` object to return just the month of the date as an `Integer`.

```ruby
require "date"
t = Date.today
pp t.month
```
{: .repl #date_month title="Date.today.month" points="1"}

### day 

Call the `day` method on a `Date` object to return just the day of the date as an `Integer`.

```ruby
require "date"
t = Date.today
pp t.day
```
{: .repl #date_day title="Date.today.day" points="1"}

In the graded code block below, write a program to identify different parts of today's date and print a `String` result. For any given date, the output should be:

"The year is: XXXX, the calendar day is: X, and the month is: X."

Use the _exact same copy_ ("The year is..."), but replace "X" with your calculated date. Don't forget to `require "date"`.

When you think you've got it, there are two tests to check the result.

```ruby
# write your program here
```
{: .repl #date_formatted title="Format the Date"}

```ruby
describe "Format the Date" do
  it "outputs 'The year is: 2020, the calendar day is: 1, and the month is: 7.' when today is July 1, 2020" do
    # Set today's date to 2020-07-01
    allow(Date).to receive(:today).and_return Date.new(2020,07,01)
    path = "/tmp/code.rb"
    expect { require_relative(path) }.to output(/The year is: 2020, the calendar day is: 1, and the month is: 7./).to_stdout
  end
end
```
{: .repl-test #date_formatted_test_1 for="date_formatted" title="Format the Date outputs 'The year is: 2020, the calendar day is: 1, and the month is: 7.' when today is July 1, 2020" points="1"}

```ruby
describe "Format the Date" do
  it "outputs 'The year is: 2020, the calendar day is: 29, and the month is: 6.' when today is June 29, 2020" do
    # Set today's date to 2020-06-29
    allow(Date).to receive(:today).and_return Date.new(2020,06,29)
    path = "/tmp/code.rb"
    expect { require_relative(path) }.to output(/The year is: 2020, the calendar day is: 29, and the month is: 6./).to_stdout
  end
end
```
{: .repl-test #date_formatted_test_2 for="date_formatted" title="Format the Date outputs 'The year is: 2020, the calendar day is: 29, and the month is: 6.' when today is June 29, 2020" points="1"}

### Date.parse 

The `Date.parse()` method accepts a `String` argument and tries to interpret it as a date, initializing a `Date` object.

```ruby
require "date"
pp Date.parse("2001-02-03")
pp Date.parse("20010203")
pp Date.parse("3rd Feb 2001")
```
{: .repl #date_parse title="Parse the Date" points="1"}

It's pretty smart!

### Subtraction 

You can subtract two dates from one another, which will return the number of days between them. The return value class is a `Rational`, which can be converted to a regular `Integer` with `.to_i`:

```ruby
require "date"

number_of_days = Date.today - Date.parse("July 4, 1776")

pp number_of_days
pp number_of_days.class

pp number_of_days.to_i
```
{: .repl #date_math title="Date math" points="1"}

In the graded code block below, write a program that uses `Date` math to output the number of days since Ruby was released on December 21, 1995. There are two tests to pass below the graded code block. Your output should look like:

"Ruby is X days old!"

Use the _exact same copy_ ("Ruby is..."), but replace "X" with your calculated number of days. Don't forget to `require "date"`.

```ruby
# write your program here
```
{: .repl #days_since_ruby title="Ruby released"}

```ruby
describe "Ruby released" do
  it "outputs 'Ruby is 8959 days old!' when today is July 1, 2020" do
    # Set today's date to 2020-07-01
    allow(Date).to receive(:today).and_return Date.new(2020,07,01)
    path = "/tmp/code.rb"
    expect { require_relative(path) }.to output(/Ruby is 8959 days old!/).to_stdout
  end
end
```
{: .repl-test #days_since_ruby_test_1 for="days_since_ruby" title="Ruby released outputs 'Ruby is 8959 days old!' when today is July 1, 2020" points="1"}

```ruby
describe "Ruby released" do
  it "outputs 'Ruby is 1 days old!' when today is December 22, 1995" do
    # Set today's date to 1995-12-22
    allow(Date).to receive(:today).and_return Date.new(1995,12,22)
    path = "/tmp/code.rb"
    expect { require_relative(path) }.to output(/Ruby is 1 days old!/).to_stdout
  end
end
```
{: .repl-test #days_since_ruby_test_2 for="days_since_ruby" title="Ruby released outputs 'Ruby is 1 days old!' when today is December 22, 1995" points="1"}

## Time

Ruby has a `Time` class as well (pre-loaded like `String`, no need to `require` anything), that shares most of its methods with the `Date` class. Rather than `Date.today`, we write `Time.now`, which makes sense. By default, it will return the time in [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

```ruby
pp Time.now
pp Time.now.class

pp Time.now.year
pp Time.now.day
pp Time.now.hour
```
{: .repl #time title="Time.now" points="1"}

### strftime 

The `strftime` method is used on a `Date` or `Time` object. It requires a `String` argument that will be used to format the `Date` or `Time` in a particular way.

You should **not** try to memorize what these patterns mean. Tools like [strftime.net](http://www.strftime.net) and [For a Good Strftime](https://www.foragoodstrftime.com/) exist to help compose the formatting string argument.

```ruby
# weekday
pp Time.now.strftime("%A")

# month
pp Time.now.strftime("%B")

# month abbreviated
pp Time.now.strftime("%b")

# weekday abbreviated, day of month, time and minutes with AM/PM
pp Time.now.strftime("%a %e, %R %p")
```
{: .repl #strftime title="strftime" points="1"}

##  Conclusion

That's it for `Date` and `Time`. Next up, we'll learn how we can make lists of data with the `Array` class.

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }

<span style="font-size: large">**When you are done here, close the window and return to Canvas for the next lesson in the series.**</span>

----
