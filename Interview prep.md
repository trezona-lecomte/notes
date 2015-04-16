# Interview Prep #

 - Remember to bring multiple copies of cover letter/resume
 - Bring laptop (fully charged), whiteboard markers, pens, 

## Questions to ask ##
I have seen that you've had at least 90% customer satisfaction for 6 years running. What do you think are the biggest contributing factors that have led to this?

I notice that you've got a public API. What are your goals for this? Strengthening your market position, extending your market reach, discovery of new markets?

What kind of projects do you have coming up? What will I be working on?

You seem to be expanding quite rapidly. Do you have any specific strategies for maintaining the close-knit team culture as the number of employees grows?

What kind of toys do we get? Hardware, furniture etc.

What can I do between now & my start date to ensure I can hit the ground running (both with RoR *and the electricity retailer domain*)?

How big are your teams? 

How do you gather & communicate requirements?

What's the process for trying out new ideas?

(maybe) can I see the desk where I'll be working please?

What will my average work-day look like once I'm out of dev-train?

Do you peer review *all* code or just some?

What does your automated regression test suite look like?

How do you approach estimates?

How do you evaluate productivity?

How do you split maintenance/new project work?

Are the work hours flexible?



## Questions to be prepared for ##

What was your experience like at your current job?

Why do you want to work for us?

What do you know about us?

Why do you want to leave your current job?

TECHNICAL:

Write code under pressure. Have someone watch you write code. Solve a kata in front of 3 people. Write tests as part of a kata. Many ruby shops will expect you to do simple problems and do them elegantly.

Explain how (almost) everything is an object in Ruby?

what does self mean when used in a class?

Explain what a ||= b means?

What are Gems and which are some of your favorites? 

What is the difference between a class and a module?

How does a symbol differ from a string?

Explain the difference between a has_one and belongs_to association?

Explain a polymorphic association?

What is a Proc?

What is a lambda? 

What are the three levels of method access control for classes and what do they signify? What do they imply about the method? 

Explain what functional testing is?

# 1. Implement your own Enumerable#map
    def map(array, &block)

    end


# 2. Implement your own Enumerable#inject
    def inject(initial, array, &block)

    end


# 3. Now, re-implement your map method
# as a single call to (your) inject


Know the differences between while, .each, upto, downto, times etc.

Know how to use yield with blocks.

know how to use .call with blocks.

Be comfortable with Array, Hash, Set and Range.

ENUMERABLES AT A MINIMUM:
 - .each_with_index
 - .inject
 - .map
 - .select

Understand *why* $Global variables are undesirable and *why* you almost never want to use @@class_variables.

Understand SOLID and how it applies to Ruby.

The *law of demeter* is your friend!

Understand the HTTP request/response cycle.  Do you know what an HTTP request looks like?  It's all human-readable and in plain text, so the answer to this is very concrete.  Have you even seen a raw HTTP request before?

Understand the difference between "the internet" and "the web"
Be able to answer the ol' cliché: "Tell me what happens when you type http://codeunion.io into your browser's URL bar and press enter."

ActiveRecord: know how it relates to SQL and how to use it idiomatically.  See jfarmer/theory_of_learning.md for an overview of ActiveRecord.  Don't be sloppy with validations and associations, either.

Schema design: know how to design a properly normalized database schema and how to identify whether a database schema is well-designed or not.
Form helpers and nested forms.  They kind of suck, but they're everywhere in Rails-land.

Know common bugs like "What is the n+1 selects issue?"  Avoid them and know how to identify and verify them when they're present.

Know where all the parts of a Rails application live.  What goes where and why?

Know what aspects of Rails are there for conventional or historical reasons, especially if they're part of the "Rails magic," e.g., auto-pluralizing model names to derive the underlying database table name.

What are the benefits of using active records as opposed to native SQL queries. On which occasion should you be choosing one over the other?

 Explain how RoR scaffolding works and why you would want to use them 

 Give some examples of RoR conventions over configurations options

 Explain Rails DB Migrate, and the benefits that comes along with that

 What are some ActiveRecords callbacks which you are familiar with ? 

 What are the difference between rails template, sub-templates and view helpers  ?

 What does Session and Cookies represent in Ruby on Rails?

 What is the function of ORM in Ruby on Rails?

 What is the difference between render and redirect? - Ruby on Rails

 What is the difference between Static and Dynamic Scaffolding? - Ruby on Rails

How can you dynamically define a method body? Why would you do this?

What is the difference between ’&&’, ‘and’ and ’&’ operators?

Does Ruby support multiple inheritance?

How can you achieve the same effect as multiple inheritance using Ruby? What is mixin?

How will you implement a singleton pattern?

How will you implement an observer pattern?

How can you define a custom Exception?

What is the default access modifier (public/protected/private) for a method?

What is scope? (or named_scope in Rails 2.x).

What is a sweeper?

How can you implement caching in Rails?

What is a filter? When it is called?

What do controllers do in Rails?

What is RESTful routing?

What is the purpose of layouts?

How can you create a REST API for your application?

How can you define a new environment called 'staging’?

What is the difference between has_one and belongs_to?

What is eager loading?

How does validation work?

What is flash?

How can you safeguard a rails application from SQL injection attack?

How can you secure a rails application?

How can rails engage with a SOA platform?





## Tips for problem solving ##

 - Ask clarifying questions
     + Context - try to get to a clear end result
     + Restrictions - language, data types, networked/non-networked
     + Assumptions - non-functional requirements
 - Look at the problem from multiple angles
 - Look for the 'why' behind the question, as well as the 'how'