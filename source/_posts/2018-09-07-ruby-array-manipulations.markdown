---
layout: post
title: "Ruby Array manipulations"
date: 2018-09-07 19:59:26 +0530
comments: true
categories: [Ruby]
---

We will be discussing some built-in functions in Ruby.Most of them are used to fix the logical challenges in Ruby Programing.

#### select
- used to filter the collections.
- return type will be an array
```
  [1, 2, 3, 4, 5].select{ |i| i > 3 }

  #=> [4, 5]
```

#### detect
- will return the first matched value
- returned value will be a single element

 ```
  [1, 2, 3, 4, 5].detect{ |i| i > 3 }

  #=> 4
 ```

#### reject
- will be the opposite of the select
- will be an array

```
  [1, 2, 3, 4, 5].reject{ |i| i > 3 }

  #=> [1, 2, 3]
```

#### equality operator
 - denoted by **===**
 - more used in the case of Reg ex and range

 ```
  (1..3) === 2

  #=> true

  (1..3) === 4

  #=> false

  /el/ === 'Hello World'

  #=> false
 ```
 - LHS should be Range or REGEX and RHS will be the specific object.

#### grep
- same use in the case of grep
```
  [6, 14, 28, 47, 12].grep(5..15)

  #=> [6, 14, 12]
```
- we have an array like [1, 'a', 'b', 2]
- if we do the ```[1, 'a', 'b', 2].map(&:upcase)```
- will raise an error
- we can fix those by **grep**

```
  [1, 'a', 'b', 2].grep(String, &:upcase)

  #=> ['A', 'B']
```
#### sort
- if we have integer and strings in the array .sort command will fail.
- we can clear this issue by using the sort_by method.

```
  ['5', '2', 3, '1'].sort_by(&:to_i)

  #=> ['1', '2', 3, '5']
```
#### all?
- return true if all values are true

```
  [2, 4, 6, 8].all?(&:even?)

  #=> true
```

#### any?
- return true if any of the value is true.

```
  [2, 3, 5, 9].any?(&:even?)

  #=> true
```

#### reduce
- create a sum of the array

```
  [1, 2, 3].reduce(:+)

  #=> 6
```
another interested methods are **cycle, next, reverse_cycle **
