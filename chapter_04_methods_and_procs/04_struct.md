# Structs

```crystal
struct User
  property name, age

  def initialize(@name : String, @age : Int32)
  end

  def print
    puts "#{age}-#{name}"
  end
end

user = User.new("Donald", 42)
user.name
user.age
user.print

# Structs are copied when passed.
def no_change(user)
  user.age = 50
end

def change(user)
  user.age = 50
  user
end


no_change(user)
user.print

updated_user = change(user)
updated_user.print
```
