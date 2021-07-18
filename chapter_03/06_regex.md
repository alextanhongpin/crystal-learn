# Regex


## Match

```crystal
str = "carbonantimonygolddiamond"
pattern = /gold/

# Returns the position of gold, otherwise nil if there's no match.
p str =~ pattern

pat = /(.+)gold(.+)/
str =~ pat
matches = str.match pat
p matches
```

## Sub

```crystal
base_currency = "USD"
currency = "GBP"
line = "<title> 1 USD = 0.7402487 GBP</title>"

regex = {
  :open => /<title> 1 #{base_currency} = /,
  :close => / #{currency}<\/title>/
}

rate = line.gsub(regex[:open], "").gsub(regex[:close], "").to_f
```
