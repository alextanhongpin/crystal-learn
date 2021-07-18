# Methods

## Named arguments
```crystal
def add(x : Int32, y : Int32)
  x + y
end

add(y = 10, x = 10)
add 10, 20 # Works without brackets
```

## Multiple return values

```crystal
def triple_and_array(s)
  {s*3, s.split}
end

num, arr = triple_and_array("hello world")
p num
p arr
```

## Splat arguments

To gather all arguments as an array.

```crystal
def salaries(*employees)
  employees.each do |emp|
    p "#{emp}'s salary is 2500"
  end
end

salaries("john", "jane", "jessie")
```

## All arguments after * must be named.

```crystal
def display(n, *, height, width)
	"#{n}: the shape has height #{height} and width #{width}"
end

p display(3, height: 10, width: 5)
```


## Giving named parameter another name.

```crystal
def increment(number, by value)
  number + value
end

p increment(10, by: 5)
```

## With last arg

```crystal
def join(*args, with joiner)
	String.build do |str|
    args.each_with_index do |arg, index|
      str << joiner if index > 0
      str << arg
    end
  end
end

join("this", "is", "awesome", with: "*")
```

## Unsplat

```crystal
def add(m, n)
  m + n
end

tup = {3, 10}
add *tup
```

## Splat named

```crystal
def add(**arg)
  arg[:m] + arg[:n]
end

tup = {m: 1, n: 2}
add(**tup)
```
