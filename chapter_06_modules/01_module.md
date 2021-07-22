# Module

## Using module as namespace

```crystal
module Crystal
  class Rhombic
  end

  class Triclinic
  end
end

min1 = Crystal::Rhombic.new
p min1

min2 = Crystal::Triclinic.new
p min2
```

## Extending itself

```crystal
module Trig
  PI = 3.142

  # Without self, the method is not accessible
  def self.add(a, b)
    a + b
  end
end

Trig.add(10, 20)

module Trig2
  extend self

  def add(a, b)
    a + b
  end
end
Trig2.add(10, 20)
```

## Mixing in modules

```crystal
module Debug
  def who_am_i?
    "#{self.class.name}#{self.object_id} #{self.to_s}"
  end
end

class User
  include Debug

  def initialize(@name : String)
  end

  def to_s
    @name
  end
end


u = User.new("john")
p u.who_am_i?
```

## Using module method on the class

```crystal
module Debug
  def who_am_i?
    "#{self.class.name} #{self.to_s}"
  end
end

class User
  extend Debug

  def initialize(@name : String)
  end

  def to_s
    @name
  end
end

User.who_am_i?
```
