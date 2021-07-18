# Fiber

```crystal
chan = Channel(String).new
num = 10_000
num.times do |i|
  spawn do
    chan.send "fiber #{i}: I like crystals!"
  end
  puts chan.receive
end
```
