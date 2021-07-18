# Yield, blocks and procs

## Yield

```crystal
def testing
  puts "at top of method"
  yield

  puts "back inside of method"
  yield

  puts "at end of method"
end

testing do
  puts "in code block"
end
```

## With Arguments

```crystal
def testing
  puts "start"
  yield 1

  puts "middle"
  yield 2

  puts "end"
end

testing do |n|
  puts "got #{n}"
end
```

## With return values

```crystal
def testing
  puts "start"
  p yield 1

  puts "middle"
  p yield 2

  puts "end"
end

testing do |n|
  puts "got #{n}"
  n + 1
end
```

## as Proc

```crystal
def testing(&block)
  puts "start"
  block.call
  puts "end"
end

testing do
  puts "hello"
end
```

## Blocks

```crystal
langs = %w[Java Go Crystal]
langs.map{|lang| lang.upcase}
langs.map &.upcase

nums = [42, 43, 44]
nums.map{|n| n + 2}
nums.map &.+(2)
```

## Proc

```crystal
# Proc literal.
fn = -> (n: Int32, m: Int32) { n + m }
typeof(fn)
fn.call(10, 20)

def add(m, n)
  m + n
end

# Using existing method.
fn = ->add(Int32, Int32)
fn.call(10, 20)
```

## Recursive Method

```crystal
def fact(n)
  n == 0 ? 1 : n * fact(n-1)
end

fact(5)

```

With error handling:
```crystal
def fact(n : Int)
  if n < 0
	  raise("n cannot be negative")
	end
	n == 0 ? 1 : n * fact(n-1)
end

fact(5)

begin
	fact(-1)
rescue ex
	p ex.message
end
```
