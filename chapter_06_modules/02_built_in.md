# Built-in modules

## Comparable

```crystal
class Person
  include Comparable(Person)

  getter name, age

  def initialize(@name : String, @age : Int32)
  end

  def <=> (other : self)
    self.age <=> other.age
  end
end

john = Person.new("john", 10)
jane = Person.new("jane", 20)
p john <=> jane
```

## Enumerable

```crystal
class Sequence
  include Enumerable(Int32)

  def initialize(@top : Int32)
  end

  def each
    0.upto(@top) do |num|
      yield num
    end
	end
end

seq = Sequence.new(10)
p seq.to_a
p seq.select &.even?
seq.map {|n| n * 2}
```
