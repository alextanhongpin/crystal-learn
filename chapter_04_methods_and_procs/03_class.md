# Class

```crystal
class Mineral
  getter name : String
  getter hardness : Float64
  getter crystal_struct : String

  def initialize(@name, @hardness, @crystal_struct)
  end
end

def mineral_with_crystal_struct(minerals, crystal_struct)
  minerals.find {|m| m.crystal_struct == crystal_struct }
end

def longest_name(minerals)
  minerals.map {|m|m.name}.max_by{|name|name.size}
end

minerals = [
  Mineral.new("gold", 1.0, "cubic"),
  Mineral.new("topaz", 8.0, "orthorombic"),
  Mineral.new("apatite", 5.0, "hexagonal"),
  Mineral.new("wolframite", 4.5, "monoclinic"),
  Mineral.new("calcite", 3.0, "trigonal"),
  Mineral.new("diamond", 10.0, "cubic")
]

min = mineral_with_crystal_struct(minerals, "hexagonal")
if min
	puts "#{min.crystal_struct} - #{min.name} - #{min.hardness}"
else
	puts "No mineral found with this crystal structure"
end

min = mineral_with_crystal_struct(minerals, "hello")
if min
	puts "#{min.crystal_struct} - #{min.name} - #{min.hardness}"
else
	puts "No mineral found with this crystal structure"
end

puts longest_name(minerals)
```

## Generic

```crystal
class Mineralalg(T)
  getter name

  def initialize(@name : T)
  end
end


min1 = Mineralalg.new("gold")
min2 = Mineralalg.new(42)
min3 = Mineralalg(String).new(42)
```

## Class Instance

```crystal
class Mineral
  # Double @ indicates class variable, as opposed to instance variable.
  @@planet = "Earth"

  def self.planet
    @@planet
  end
end

Mineral.planet
```

## Read-only, write-only and property

```crystal
class Mineral
  # Read-only values.
  getter name, hardness, crystal_struct

  # Write-only values.
  setter id

  # Both read and write only.
  property quantity : Float32
  def initialize(@id : Int32, @name : String, @hardness : Float64, @crytal_struct : String, @quantity = 0f32)
  end
end

min = Mineral.new(101, "gold", 1.0, "cubic")
min.id = 100
min.quantity = 200
min.name

# Create shallow copy.
mindup = min.dup
mindup == min
```

## Inheritance

```crystal
class Document
  property name

  def initialize(@name : String)
  end

  def print
    puts "Hi, I'm printing #{name}"
  end
end


class PDFDocument < Document
end

pdf = PDFDocument.new("Price History")
pdf.print

```

## Super class

```crystal
class Document
  property name

  def initialize(@name : String)
  end

  def print
    puts "Hi, I'm printing #{name}"
  end
end


class PDFDocument < Document
  def initialize(@name : String, @company : String)
  end

  def print
    super
    puts "From company: #{@company}"
  end
end

pdf = PDFDocument.new("Price History", "ABC")
pdf.print

```

## Abstract Class

```crystal
abstract class Shape
  abstract def area
  abstract def perim
end

class Rect < Shape
  def initialize(@width : Int32, @height : Int32)
  end

  def area
    @width * @height
  end

  def perim
    2 * (@width + @height)
  end
end

rect = Rect.new(10, 20)
rect.area
rect.perim
```

## Polymorphism

```crystal
# Without abstract class, we can't do d.doc.print
# class Document
abstract class Document
end

class PDFDocument < Document
  def print
    puts "PDF header"
  end
end

class XMLDocument < Document
  def print
    puts "XML header"
  end
end

class Report
  getter doc

  def initialize(@name : String, @doc : Document)
  end
end

pdf = Report.new("product price", PDFDocument.new)
xml = Report.new("product price", XMLDocument.new)

if true
	d = pdf
else
	d = xml
end

typeof(d)
d.doc.print
```

##  Private method

```crystal
class Document
  property name

  def initialize(@name : String)
  end

  private def print(message)
    puts message
  end

  def printing
		# self.print (Does not work, however it works with protected method).
    print "Hi, I'm #{@name}"
  end
end

class PDFDocument < Document
  def printing
    super
    print "End printing PDF Document"
  end
end

doc = Document.new("salary range Q4")
doc.printing
# doc.print Error

pdf = PDFDocument.new("salary range Q4")
pdf.printing
# pdf.print Error
```

## Protected method

```crystal
class Document
  property name

  def initialize(@name : String)
  end

  protected def print(message)
    puts message
  end

  def printing

    print "Hi, I'm #{@name}"
    self.print "this works too"
    doc = Document.new("inside document")
    doc.print("works")
  end
end

class PDFDocument < Document
  def printing
    super
    print "End printing PDF Document"
  end
end

doc = Document.new("salary range Q4")
doc.printing

pdf = PDFDocument.new("salary range Q4")
pdf.printing
# pdf.print Error

# print works because it's a subclass of Document.
class BankAccount < Document
  def printing
    doc = Document.new("test bank account")
    doc.print("works for bank account")
  end
end
b = BankAccount.new("hello")
b.printing

# print does not work because it's not a subclass of Document.
class BankAccount2
  def printing
    doc = Document.new("test bank account")
    doc.print("works for bank account") # Error: protected method print called for Document
  end
end
b = BankAccount2.new
b.printing
```

## Overloading operators

```crystal
class Mineral
  getter id, name, hardness, crystal_struct
  property quantity : Float32

  def initialize(@id : Int32, @name : String, @hardness : Float32, @crystal_struct : String, @quantity = 0f32)
  end

  def ==(other : self) # self is mineral
    id == other.id
  end

  def ==(other)
    false
  end

  def self.compare(m1 : self, m2 : self)
    m1.id == m2.id
  end
end


m1 = Mineral.new(101, "gold", 1.0, "cubic")
m2 = Mineral.new(108, "gold", 1.0, "cubic")
m3 = Mineral.new(101, "gold", 1.0, "cubic")
m1 == m2
m1 == m3
Mineral.compare(m1, m2)
m1 == 2
```

## Multiple initialize

```crystal
class Mineral
  getter id, name, hardness, crystal_struct
  property quantity : Float32

  def initialize(@id : Int32, @name : String, @hardness : Float32, @crystal_struct : String, @quantity = 0f32)
  end

  def initialize(@id : Int32)
    @quantity = 0f32
    @name = "rock"
    @hardness = 0
    @crystal_struct = "unknown"
  end
end

m1 = Mineral.new(101, "gold", 1.0, "cubic")
m2 = Mineral.new(1)
```
