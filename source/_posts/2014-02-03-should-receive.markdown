---
layout: post
title: "should_receive"
date: 2014-02-03 19:40:39 -0500
comments: true
categories: [rails, rspec, ruby]
---
The other day I ran into some issues using the should_receive method provided by RSpec (in
`Spec::Mocks::Methods`). I was using it in a controller spec to test that a model was receiving the
appropriate method call. I'm still not sure if I like using this type of check in a test or not,
but I guess that's a topic for another post.

My test was equivalent to something like this:
```ruby
it 'creates a new post' do
  Post.should_receive(:new).with('title' => 'TestTitle')
  post :create, post: { 'title' => 'TestTitle' }
end
```

The error I was getting was:
```
NoMethodErrror: undefined method 'save' for nil:NilClass
```

<!-- more -->

While I haven't had a chance to dig into the source code yet, I have a pretty good idea of what's
causing this error based on the behavior I've seen.

So what I believe is happening, is that when the should_receive is used on a class, the method it
specifies is either intercepted or stubbed in some way such that it returns nil. In my issue above,
within my control when it calls 'new' it gets a nil object back. It then calls save on the nil
object (the controller is just the default rails 4 generated controller) and we get the error above.

There are a few ways to solve this issue, the easiest is probably to mock the object returned by
new. Here's what that would look like:
```ruby
it 'creates a new post' do
  p = mock_model(Post).as_null_object
  Post.should_receive(:new).
    with('title' => 'TestTitle').
    and_return(p)
  post :create, post: { 'title' => 'TestTitle' }
end
```

The RSpec method `as_null_object` makes it so that the object can be passed any message and not
throw an error. So now we have the Post.new returning a mock object that can accept any message, so
when save is called, while it doesn't do anything, it also doesn't throw any exceptions.
