## Week One - Module 2 Recap

Fork this respository. Answer the questions to the best of your ability. Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week (which is a TON!). 

Note: When you're done, submit a PR. 

### Week 1 Questions

1. List the five common HTTP verbs and what the purpose is of each verb.
* `GET` - Reads copy of resource
* `POST` - Creates new resource
* `PUT` - Updates an entire new version of a resource
* `PATCH` - Updates a portion of a resource
* `DELETE` - Destroys a resource

2. What is Sinatra?
* Sinatra is a server-side web framework that works with Ruby and ActiveRecord in the Model/View/Controller way of organizing a web application, using the MVC style of organizing a server HTTP responsibilites.
3. What is MVC?
* A Controller receives an HTTP request from a client/browser, communicates any necessary portions of that request to a Model, which may interact with a Database/Databases and send any requested info back to the Controller. The Controller then sends the relevant information to the View(s) to render properly and finally sends the rendered page back to the browser.
4. Why do we follow conventions when creating our actions/path names in our Sinatra routes?
* It allows for ease of other developers finding information in our app when they come onto a pre-existing project or codebase.
5. What types of variables are accessible in our view templates without explicitly passing them?
* Anything in the address bar, anything we've associated in our models/databases via ActiveRecord
6. Given the following block of code, how would I pass an instance variable `count` with a value of `1` to my `index.erb` template?
  
  ```ruby
  get '/horses' do
    @count = 1
    name = 'Mr. Ed'
    @something = something.find(params[:name])
    erb :index
  end
  ```
8. In the same code block, how would I pass a local variable `name` with a value of `Mr. Ed` to the view?
* See above. I'm unsure how you could pass any local information from the controller to a view without assigning it somehow to an instance variable for the view to have access to it.
9. What's the purpose of ERB?
* Enhanced RuBy allows you to access and manipulate data through Ruby syntax and render it into HTML
10. Why do I need a development AND test database?
* You don't want any of your methods or HTML verbs to actually destroy information from your database or modify it while you are refining them. It is also faster to be able to check smaller datasets for whatever capabilities you are creating for your app.
11. What is CRUD and why is it important?
* Create, Read, Update, Delete (CRUD) is the basic functionality all applications that deal with datasets/databases typically provide a user. It's ReSTful design, which is more universally agreed upon to be the best and the standard for web development.
12. What does HTTP stand for?
* HyperText Transfer Protocol. It's the rules that govern how the web works/data packets are sent and received between clients and servers.
13. What are the two ways to interpolate Ruby in an ERB view template? What's the difference between these two ways?
* `<% #Invsible Ruby code here %>` or `<%= #Visible Ruby code here %>`. The equal sign after the initial percentage symbol means whatever the result of the code to follow is going to be rendered to the screen and converted/inserted into the HTML document.
14. What's an ORM?
* Object Relational Mapper
15. What's the most commonly used ORM in ruby (Sinatra & Rails)?
* ActiveRecord
16. Let's say we have an application with restaurants. There are seven verb + path combinations necessary to provide full CRUD functionality for our restaurant application. List each of the seven combinations, and explain what each is for.
* `get '/'` gets us to the homepage <-- _not necessarily part of the 7, but important nonetheless_
* `get '/restaurants'` gets us to the index/list of restaurants in the database (an :index view in .erb)
* `get '/restaurants/new'` takes us to the create new restaurant form page (a :new view in .erb)
* `post '/restaurants'` allows us to create a new restaurant in our database (and redirects to the main index as long as you code it in the block)
* `get '/restaurants/:id'` allows us to go to an individual restaurant page (a :show view in .erb)
* `get '/restaurants/:id/edit'` takes us to the edit current restaurant form (an :edit view in .erb)
* `put '/restaurants/:id'` edits/updates the existing restuarant in our database according to whatever was put in the form (and redirects to index as long as you code it in the block)
* `delete '/restaurants/:id'` destroys the current restaurant from our database (and redirects to index as long as you code it  in the block)
17. What's a migration? 
* It's when you add a table to your database or modify the structure of an existing table in your database.
18. When you create a migration, does it automatically modify your database?
* No, you have to `rake db:migrate` after you `rake db:create_migration NAME='new_migration'`
19. How does a model relate to a database?
* It's the thing responsible for interacting with the data in there. Migrations `change` the database by adding or modifying tables within it, and the resulting `schema` are the parameters that the Model has to work with when calling portions of the data for the Controller. Models can require verifications/validations of the data to ensure no unwanted `nill` values are passed to or from the database/dataset and can have `class methods` that use ActiveRecord's library of methods to perform calculations with the data.
20. What is the difference between `#new` and `#create`?
* `#new` provides a local instance of a class to play with whereas `#create` creates a dataset within a database (like a row).
### Review Questions:  
21. Given a CSV file (“films.csv”) with these headers [id, title, description], how would you load these into your database to create new instances of Film? 
* I would run:
```
rake db:create_migration NAME='create_films'
```
* Then, in the migration file, I would code the following:
```
# create Films table
class CreateFilms < ActiveRecord::Migration[5.2]
  def change
    create_table :films do |t|
      t.string :title
      t.text :description

      t.timestamps
    end
  end
end
```
* I would create a seeds.rb file in the root of the db directory with the following information:
```
csv = File.read('films.csv', headers: true, header_converters: :symbol)
csv.each do |line|
  Film.create(id:          line[:id],
              title:       line[:title],
              description: line[:description])
```
* Then I would run the migration and seed operations
```
rake db:migrate
rake db:seed
```
* If needed, I would run `rake db:environment:set` and `rake:test:prepare` during/afterwards
22. Given the following hash:
```
activities = {
  hiking: {cost: $0, supplies: ['hiking shoes', 'water', 'compass']},
  karaoke: {cost: $10, supplies: ['courage', 'microphone'],
  brunch: {cost: $35, supplies: ['mimosa flutes'],
  antiquing: {cost: $200, supplies: ['list of antique stores'] 
}
```
How would I add 'granola bar' to things you should have when hiking?
* `activities[:hiking][:supplies] << 'granola bar'`
23. What are the 4 Principles of OOP? Give a one sentence explanation of each.
* Proper Encapsulation - Variables should not be exposed outside of methods or classes by accessors or mutators unless absolutely necessary
* Data Abstraction - creating models of real things/data that have all the essential characteristics of those real things/data. Breaking things down into the smallest possible step/role/characteristic (aka, single responsibility principle - a method should do only one thing)
* Polymorphism - 'one name, many forms' - having multiple methods with the same name but slightly different functionality. In this way, a superclass can contain a default method that all of its subclasses inherit, while a particular subclass can override that default method to do something specific to its own class.
* Inheritance - Objects relate to one another in a 'has a', 'uses a' or 'is a' relationship. Inheritance is the 'is a' one. This allows superclasses to hold more general states and behaviors while classes and modules hold more specific states and behaviors and c more specific.

### Self Assessment:
Choose One:
* I was able to answer most questions independently, but utilized outside resources for a few

Choose One:
* I feel confident about the content presented this week
