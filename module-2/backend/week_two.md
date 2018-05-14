## Week Two - Module 2 Recap

Fork or re-pull this respository. Answer the questions to the best of your ability. Try to answer them with limited amount of external research. These questions cover the majority of what we've learned this week (which is a TON - YOU are a web developer!!!). 

Note: When you're done, submit a PR.


### Week 2 Questions

1. At a high level, what is ActiveRecord? What does it do/allow you to do?
* ActiveRecord is a library of methods that allows for quick database queries and associations. It operates in Sinatra and Rails environments.

2. Assume you have the following model:
```ruby
class Team << ActiveRecord::Base
end
```
What are some methods you can call on `Team`? If these methods aren't defined in the class, how do you have access to them?
* ActiveRecord is being assigned as a superclass to Team with the <<, so Team has access to all of its methods, like join, select, find, find_by, group_by, order, etc.

3. Assume that in your database, a team has the following attributes: "id", "name", owner_id". How would you find the name of a team with an id of 4? Assuming your class only included the code from question 2, how could you find the owner of the same team?
* `Team.find(4)`
* `Team.find(4).owner_id` would give you the owner_id of the owner. Then you could do Owner.find(Team.find(4).owner_id)

4. Assume that you added a line to your `Team` class as follows:
```ruby
class Team << ActiveRecord::Base
  belongs_to :owner
end
```
Now how would you find the owner of the team with an id of 4?
* Assuming that you've also setup a has_many relationship within Owner, you could do Owner.teams(4)

5. In a database that's holding students and teachers, what will be the relationship between students and teachers? Draw the schema diagram.
* It would be a many to many relationship
__Students__ __StudentsTeachers__ __Teachers__
id            id                   id
name          student_id           name
              teacher_id
              
6. Define foreign key, primary key, and schema.
* Foreign key is the foreign id present on the end of a table that associates one table with a different one.
* Primary key is the id that the database language incrementally assigns a table row
* Schema is the blueprint of your database, listing each table and its attributes/column headers and data types within those columns

7. Describe the relationship between a foreign key on one table and a primary key on another table.
* The foreign key on one table will always be the primary key on another table.

8. What are the parts of an HTTP response?
* Header and body of the response. The header has the protocol and the response message code (ex: 200 OK), the body has the metadata like the browser, view pane size of the browser, IP address of the recipient, etc.

### Optional Questions

1. Name your five favorite ActiveRecord methods (i.e. methods your models inherit from ActiveRecord) and describe what they do.
* `find(#)` finds an element by its primary key id.
* `find_by` finds an element by something other than its primary key id.
* `all` calls all the instances of a class, which can be assigned to a method.
* `order_by` orders the database by a column header in ascending (ASC) or descending order (DESC) 
* `where` finds all the instances of a table that match a specific set of conditions

2. Name your three favorite ActiveRecord rake tasks and describe what they do.
* `rake db:create_migration NAME="create models table"` creates a migration where you can add a table with columns and specific data types to your db. The name of the table must always be plural.

3. What two columns does `t.timestamps null: false` create in our database?
* `created_at` and `updated_at`

4. In a database that's holding schools and teachers, what will be the relationship between schools and teachers?
* many to many

5. In the same database, what will you need to do to create this relationship (draw a schema diagram)?
* You would need to create a joins table called `StudentsTeachers` that would have a unique id, student_id and teacher_id. See above.

6. Give an example of when you might want to store information besides ids on a join table.
* grades for courses could exist on a separate table with `student_ids` and be in its own `grade` column.

7. Describe and diagram the relationship between patients and doctors.
* again, many to many. Patients `has_many` Doctors and Doctors `has_many` patients

8. Describe and diagram the relationship between museums and original_paintings.
* one to many, OriginalPaintings `belongs_to` a Museum.

9. What could you see in your code that would make you think you might want to create a partial?
* any repetition. Forms, layouts with the necessary header info already in there, yielding the body of the document to specific views.

### Self Assessment:
Choose One:
* I was able to answer every question without relying on outside resources

Choose One:
* I feel comfortable with the content presented this week
