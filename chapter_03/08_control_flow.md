# Control flow

## Ternary operator
```crystal
a, b = 1, 2
a > b ? "yes" : "no"
```

## Type Checking

```crystal
var1 = rand < 0.5 ? 42 : "Crystal"

ivar1 = var1.as?(Int32) # Attempt to convert to int32, otherwise nil.

# Check if truthy/falsy. Nil is falsy.
if ivar1
	p ivar1.abs
else
	p "not an integer"
end

# Check if it's a number.
if ivar1.is_a?(Number)
	p ivar1.abs
end

# Check if it's nil.
if ivar1.nil?
	p "is nil"
end
```

## Case When
```crystal
case var1
	when Number
		p "is a number"
	when String
		p "is a string"
	else
		p "not a number or string"
end


case 42
	when .even?
		p "is even number"
	when .odd?
		p "is odd number"
end


(1..100).each do |i|
  case {i%3, i%5}
    when {0, 0}
      puts "FizzBuzz"
    when {0, _}
      puts "Fizz"
    when {_, 0}
      puts "Buzz"
    else
	    puts i
  end
end
```

## Responds to

```crystal
var1 = "Crystal"
if var1.responds_to?(:abs)
	p var1.abs
end

var2 = -42
if var2.responds_to?(:abs)
	p var2.abs
end
```
