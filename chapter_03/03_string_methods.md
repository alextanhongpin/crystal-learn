# String

## String methods

```crystal
curr1 = "US Dollar"
curr1[2..4]
curr1.reverse
curr1.size
curr1.upcase
curr1.capitalize
curr1.includes? "la"
curr1.count "l"
curr1.starts_with? "Us"
curr1.ends_with? "ar"
curr1.index("a")
curr1.sub("||", "|")
curr1.gsub(/([aeiou])/, "*\\1*")
curr2 = curr1.split("")
curr2.join("-")
```

## Building string more efficiently

```crystal
rate = 0.8432
p "rate: " + rate.to_s

# String interpolation is more efficient:
p "rate: #{rate}"

# Using string builder
str = String.build do |io|
  io << "rate: " << rate
end
p str
```
