# Performance tips


## Use to_s

String is created in heap memory, and they have to be garbage collected. Avoid creating too many strings.

```crystal
class Mineral
  getter name, hardness

  def initialize(@name : String, @hardness : Int32)
  end

  def to_s(io)
    io << name << ", " << hardness
  end
end

min = Mineral.new("gold", 42)

io = IO::Memory.new
min.to_s(io).to_s
```

## Using exception as class

```crystal
class CoolException < Exception
end

raise CoolException.new("bad code")
```

## Defining callbacks

```crystal
class Mineral
  def initialize
    @callbacks = [] of ->
  end

  def after_save(&block)
    @callbacks << block
  end

  def save
  rescue ex
    p "Exception occured: #{ex.message}"
  else
    @callbacks.each &.call
  end
end

min = Mineral.new
min.after_save { puts "Save to DB successful" }
min.after_save { puts "Logging save" }
min.save
```
