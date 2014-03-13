---
layout: post
title: "Custom Model Validation"
date: 2013-09-08 13:45:14 -0500
comments: true
categories: rails
---
So far I've always been able to use the validates method within my models in Rails to handle all of
my validation needs, whether it's checking a field exists, or checking its length, max/min values,
or comparing it to a regex, model validation has been extremely easy within Rails.

The other day I had a more complex validation requirement that I was worried would be more
difficult to integrate so that it worked similarly to the existing validations in the model.
However, after a few minutes of research I discovered how easy rails makes it to do exactly what I
wanted!

<!-- more -->

The validation requirement was to run an address through a Address Verification service and report
errors as needed.

Rails made this easy with the validate method, which takes a method as a symbol for it's parameter,
like this:

```ruby
validate :validate_address
```

Then in the method, you can add custom errors, so that when these errors have been added, the model
will be considered invalid, like this:

```ruby
def validate_address
  ...
  validated = <validation service>
  if !validated
    errors.add(:base, "Address could not be verified!")
  end
  ...
end
```

This adds errors to the base you can even get more specific and add the error messages to a
specific attribute like this:

```ruby
def validate_address
  ...
  validate_status = <validation service>
  if !validate_status.address1
    errors.add(:address1, "Address could not be verified!")
  elsif !validate_status.city
    errors.add(:city, "Address could not be verified!")
  elsif ...
  end
  ...
end
```

As you can see this ability to hook into the Rails model validation makes it easy to customize the
validation of any models.
