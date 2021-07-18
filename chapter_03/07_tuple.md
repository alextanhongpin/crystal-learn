# Tuple

```
tpl = {42, "silver", 'C'}
tpl.class

a = Tuple.new(42, "silver", 'C')
p a[0]
p a[1]
p a[2]
p a[-2]
p a[100]? # => nil
# p a[100] => Index out of bounds (IndexError)
```

## Hash Set

```crystal
h = {1 => 'A'}
h[3] ||= 'C'
h[3] ||= 'D'
p h
```

## Named tuple

```crystal
tpl = {name: "Crystal", year: 2017}
p tpl.class

p tpl[:name]
```

## Set

```crystal
set = Set{1,1,2,3}
set.class
p set
set << 42
set << 1
p set

ss = Set(Int32).new
ss << 1
p ss
```
