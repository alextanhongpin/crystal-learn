# Symbol

Symbols are stored as unique int32 value, using them saves memory compared to using strings.

```crystal
class Mineral
  property name

  def initialize(@name : Symbol)
  end
end

mineral1 = Mineral.new(:talc)
mineral8547 = Mineral.new(:talc)

p mineral1.name
p mineral8547.name
mineral8547.name = :gold
p mineral8547.name
```
