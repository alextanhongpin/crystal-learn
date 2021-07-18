# Class

## Basic class

```crystal
class Mineral
  def initialize(common_name : String, hardness : Float64)
    @common_name = common_name
    @hardness = hardness
  end
end

mine = Mineral.new("talc", 1.0)
p typeof(mine) # Mineral
```

## Getter/setter

```crystal
class Mineral
  getter common_name : String
  setter common_name

  getter hardness : Float64
  def initialize(@common_name : String, @hardness : Float64)
  end
end

mine = Mineral.new("talc", 1.0)
p typeof(mine) # Mineral
p mine.common_name
mine.common_name = "ruby"
p mine.common_name
p mine
p mine.hardness
```

## With methods

```crystal
class Mineral
  getter common_name : String
  setter common_name
  getter hardness : Float64
  getter crystal_struct : String

  def initialize(@common_name, @hardness, @crystal_struct)
  end

  def describe
    "This is #{common_name} with a Mohs hardness of #{hardness} and a structure of #{crystal_struct}"
  end
end

mine = Mineral.new("talc", 1.0, "monoclinic")
p mine.describe
```

## Module

We can enhance a class by including modules.

```crystal
module Hardness
  def data
    {"talc" => 1, "calcite" => 3, "apatite" => 5, "corundum" => 9}
  end

  def hardness
    data[self.name]
  end
end

class Mineral
	include Hardness

  # This is required for the module.
  getter name : String

  def initialize(@name : String)
  end
end

mine = Mineral.new("talc")
p mine.hardness
```
