# ruby-slurry
A meddling of ruby procs with curry

```ruby
# our method
def sum(a, b)
  a + b
end

# let's curry so that we can partially apply
inc = method(:sum).curry

# fun
puts [1,2,3].map(&inc[1]).inspect #=> [2,3,4]

# predicate now
def greater_than(b, a)
  b < a
end

greater_than = method(:greater_than).curry

# partially applied predicate
puts [1,2,3,4,5].select(&greater_than[3]).inspect #=> [4,5]

# more args
between = ->(min, max, n) { min < n && n < max }.curry

# that syntax is funky, but what fun
puts [1,2,3,4,5].select(&between[1][4]).inspect #=> [2,3]

# now we're getting crazy
class Foo
  def self.sum
    lambda do |a, b|
      a + b
    end.curry
  end
end

add1 = Foo.sum[1]

puts [1,2,3].map(&Foo.sum[100]).inspect #=> [101, 102, 103]

puts Foo.sum[1, 2] #=> [3]
```

Source: https://replit.com/@miwillhite/ExtrasmallWaterloggedDatalog#main.rb
