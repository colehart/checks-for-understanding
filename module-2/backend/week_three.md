## Week Three Recap

### Week 3 Questions

1. What is the entry at the command line to create a new rails app?
> `rails new [app_name] -T -d="postgresql" --skip-turbolinks --skip-spring`
2. What do Models generally inherit from in rails?
> ApplicationRecord, which inherits from ActiveRecord::Base
3. What do Controllers generally inherit from in a rails project?
> Application Controller, which inherits from ActionController::Base
4. How would I create a route if I wanted to see a specific horse in my routes file assuming I'm sticking to standard conventions and that I didn't want other CRUD functionality?
> In `config/routes.rb`, you'd write `resources :horses, only: [:show]`
5. What rake task is useful when looking at routes, and what information does it give you?
> `rake routes` gives you a list/table of the route prefix (usable by Rails as a shorter nickname to access that URI), the associated HTML verb, the URI pattern (which gives information on what variables must be included for any nested resources, and the controller action of that route.
6. What is an example of a route helper? When would you use them?
> A route helper is the prefix given for a specific Controller action. You would use them in both:
> 1. RSpec feature tests instead of typing out the URI to `visit` or `expect(current_path).to eq(route_helper)`, and
>
> 2. In Controller actions as redirects or Views as a shorthand way to go to another Controller-Action/View.
7. What's the difference between what `_url` and `_path` return when combined with a routes prefix?
> `_url` returns the full URI, while `_path` returns the truncated/shorter version.
8. What are strong params and why are they necessary?
> Strong params are a way of properly encapsulating database queries and params from external manipulation. They are always located below the `private` section at the bottom of a Controller and shield your database from malevolent queries from the address bar.
9. What role does `form_for` play in helping us create our forms?
>`form_for` provides an ActiveRecord-friendly template of a form that eases developer creation of a table with easy-to-understand form fields and data-types, and submits user-provided information to the proper table.
10. How does `form_for` know where to submit the user's input?
> It takes the parameters supplied directly after `form_for`, either one or multiple in an array in order of nested resources, and submits the user's input through those paths/URI's to the correct table.
11. Create a form using a `form_for` helper to create a new `Horse`. 
```ruby
= form_for @horse do |f|
  =f.label :name
  =f.text_field :name
  =f.label :breed
  =f.text_field :breed
  =f.submit
```
12. Why do we want to validate our models?
> To ensure that models are not created with/do not contain `nil` values in our database.
13. What are the steps of the DNS lookup?
> client submits a request through a browser in text/web address form (ex: www.google.com) which goes through the computer OS to the DNS server where is looked up by its IP address. The DNS server then returns the IP address to the client/browser through the OS and the ISP continues to carry the request across the web via TSP to the proper server for that IP address.

### Review Questions
14. How would you call the method `prance` from within the method `move` on a `Horse` instance?
> `@horse.move.prance`
15. Given the following hash:
```ruby
furniture = {table: {height: 3, color: "red"}, purchased: true}
```
What is the different between how you would return true vs returning 3?  
> `furniture[:purchased]` would return `true`, while `furniture[:table][:color]` would return `"red"` since it's nested inside of the `table` element.

16. What is inheritance?
> It's indicated in a Ruby class by the 'less than' symbol to the right of the class name (ex: `class Example`**< ActiveRecord::Base**). The class inherits any methods or variables named by the superclass and can reassign those methods or variables if need be.

### Self Assessment:
Choose One:
* I was able to answer most questions independently, but utilized outside resources for a few

Choose One:
* I feel overwhelmed by the content presented this week

Note: being out sick on Monday was not good timing. I'm feeling better about it now but still feeling pretty far behind.
