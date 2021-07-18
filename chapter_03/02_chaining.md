# Chaining in Crystal

```crystal
result = (42..47).to_a # Range is converted to array.
.sort{|m, n| m <=> n} # Sort array in reverse order. <=> is the comparison operator.
.reject {|n| n.odd? } # Eliminate odd numbers with reject.
.map {|n| n * n} # Map
.select{|n| n % 4 == 0} # Select only numbers divisible by 4.
.tap{|arr| puts "#{arr.inspect}"} # Tap passes the object to the block and returns it - useful for debugging.
.sort!  # Sort array in-place.
.any? {|num| num > 2000} # Check if any numbers > 2000.
```

## Sum

```crystal
sum = (42...47).to_a
.reduce(0) { |sum, num| sum + num }
```
