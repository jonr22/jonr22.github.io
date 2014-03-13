---
layout: post
title: "Defined Symbols"
date: 2013-09-07 15:51:56 -0500
comments: true
categories: ruby
---
I was playing in irb and I wanted to look at the defined symbols, conveniently you can use

```ruby
Symbol.all_symbols
```

then I decided to check if some particular symbols were defined, so I ran the following command

```ruby
Symbol.all_symbols.include?(:abcde)
```

<!-- more -->

However, I immediately found it curious to see that every symbol I tried was coming up as being included in the Symbol.all_symbols array.

Thinking about it however, this make perfect sense, the symbol was defined as part of the statement I executed and therefore added to the Symbol.all_symbols array and so it was found as being included in this array.

I still wanted to be able to find if a symbol was defined (not that it particularly matters whether it's defined or not, but I was having fun) so I came up with using the any? method provided by Enumerable, and instead of looking for a symbol, I looked for the string equivalent, like so:

```ruby
Symbol.all_symbols.any? { |s| s.to_s == "abcde" }
```

I don't think this is particularly useful to many people, but I found it interesting and I think it shows how flexible Ruby is, in that I was still able to come up with a fairly simple one-line statement to accomplish what I was looking for.
