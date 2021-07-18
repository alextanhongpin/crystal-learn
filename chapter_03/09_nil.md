# Nil

```crystal
n : Int32 | Nil
n = 42
p typeof(n)

m : Int32?
m = nil
p typeof(m)

m = 42
p typeof(m)

o : Int32?
o = nil
o.try { p o + 1 }
```
