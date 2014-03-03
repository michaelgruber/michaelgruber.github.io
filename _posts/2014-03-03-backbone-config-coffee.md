---
layout: post
title: Backbone Config with CoffeeScript Sigletons
---

I've been working on a Coffee con Backbone project, and recently I've wanted a
config file for my front end code. Stack Overflow had several
[good](http://stackoverflow.com/questions/11459745/can-we-create-environment-variables-for-backbone-applications)
[solutions](http://stackoverflow.com/questions/18464413/how-to-make-a-config-file-which-i-can-include-in-my-backbone-js-project),
but once I started adapting them to CoffeeScript I decided to make use of the
CoffeeScript Cookbook's [Singleton Pattern](http://coffeescriptcookbook.com/chapters/design_patterns/singleton).
Here's what I wound up with:

### [config.js.coffee](https://gist.github.com/michaelgruber/9338251)
{% highlight coffee linenos %}
class SingletonConfig
  # Private scope
  # Ensure correct scope by setting instance to null.
  instance = null

  # This private class gets initialized by the singleton.
  class Config
    # The actual configuration attributes
    defaults:
      foo: "bar"
    development:
      foo: "baz"

    # Set up our environment specific config,
    # overriding defaults.
    constructor: (env) ->
      @config = _.extend @defaults, @[env]

    # Provide a Backbone-style shortcut to retrieve our
    # config values.
    get: (key) -> @config[key]

  # The static method to retrieve/create instance
  @get: () ->
    env = switch window.location.hostname
      when "localhost", "127.0.0.1" then "development"
      else "production"
    instance ?= new Config(env)

MyApp.Config = SingletonConfig.get()

# http://localhost:3000/
MyApp.Config.get('foo') # => baz
{% endhighlight %}

