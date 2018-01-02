# learned-today
Just a readme. To log things I learn.

## October 2017

#### 24th

- `ensure` discards its return. #ruby
	- https://stackoverflow.com/questions/1756452/how-ensure-works-in-ruby

	```
	begin
	  puts 'begin!'
	  :foo
	ensure
	  puts 'ensure!'
	  :bar
	end
	# begin!
	# ensure!
	# => :foo
	```
	
- The body of a GET request is semantically meaningless... usually. #http
	- https://stackoverflow.com/questions/978061/http-get-with-request-body

--

#### 25th

- `%r` is the custom delimiter for regex. It will auto-escape `/`s. #ruby #regex
	- https://stackoverflow.com/questions/12384704/the-ruby-r-expression
	- https://stackoverflow.com/questions/3517238/what-does-the-operator-do-in-ruby-in-n-2

	`%r(//) == /\/\// # true`

- To use Sidekiq in a local environment, start it in a shell: `bundle exec sidekiq`. #devops #ruby

| Method(s) | t | 
|----------------------------|------|
| .limit(1).first.id | 4.65 |
| .any? | 3.46 |
| .exists? | 3.24 |
| .limit(1).pluck(:id).first | 2.91 |


--
#### 27th

- `ActiveRecord::Base.exists?` executes `SELECT 1 FROM some_table LIMIT 1`

--

#### 30th

- 'Transaction isolation levels' are things that exist. #databases #rails #postgres
	- http://api.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/DatabaseStatements.html
	- https://www.postgresql.org/docs/current/static/transaction-iso.html

- You can pass raw SQL to `ActiveRecord::Calculations#pluck`

--

### 31st

- Postgres will (or can be configured to) coerce stuff to UTC regardless of what timezone it was originally in.


	```
	Time.now
	```
	

## November 2017

### 1st

- I need a better way to remember what the various time libraries in Rails actually do. Maybe a tattoo of a watch on my wrist, with a stamp that says "USE TIME.CURRENT" where the face should be. #rails #personal
- `it_behaves_like` uses a _nested_ context, `include_examples` uses the _current_ context. Use `it_behaves_like` unless you have a good reason not to. #rspec

	```
	# Tests
	RSpec.describe 'shared_examples demonstration' do
	  shared_examples '<-- this is the shared block description -->' do
	    let(:overwrittten?) { true }
	    it "overwrites inside" do
	      expect(overridden?).to be true
	    end
	  end
	
	  let(:overwritten?) { false }
	
	  describe 'include_examples' do
	    include_examples '<-- this is the shared block description -->'
	    it "does not overwrite outside" do
	      expect(overwritten?).to be false
	    end
	  end
	
	  describe 'it_behaves_like' do
	    it_behaves_like '<-- this is the shared block description -->'
	    it "does not overwrite outside" do
	      expect(overwritten?).to be false
	    end
	  end
	end
	```
	```
	# Result
	shared_examples demonstration
	  it_behaves_like
	    does not overwrite outside
	    behaves like <-- this is the shared block description -->
	      overwrites inside
	  include_examples
	    overwrites inside
	    does not overwrite outside (FAILED - 1)
	
	Failures:
	
	  1) shared_examples demonstration include_examples does not overwrite outside
	     Failure/Error: expect(overridden?).to be false
	
	       expected false
	            got true	
	```

--

### 3rd

- `reflect_on_all_associations`
	- https://www.viget.com/articles/identifying-foreign-key-dependencies-from-activerecordbase-classes

- bi-directional associations in ActiveRecord

	> Active Record supports automatic identification for most associations with standard names. However, Active Record will not automatically identify bi-directional associations that contain any of the following options:
	> 
	> :conditions
	> :through
	> :polymorphic
	> :class_name
	> :foreign_key
	
--
### 6th

- Grape serializes nil to `"null"`. (sometimes?) #rails #grape

--

### 7th

-  Monoids (in software) are a functional pattern that includes a data type and an operator or function. An isolated class, function, etc. cannot be itself a Monoid.

Meetup: ChicagoRuby
> Downtown - Building Functional Pipeline in Rails  
> https://www.meetup.com/ChicagoRuby/events/243259981

--

### 13th

- The magic string freeze comment doesn't work on Arrays.

--

### 14th

- There are various factions within the Agile commnunity and/or using the Agile brand. One such faction is Modern Agile, which defines itself as a set of goals that are agnostic to project management implementations.
	- Among critics of the original Agile system, a common criticism is that it leads to "feature mills".

Meetup: Chicago Agile Open Space
> Agile Thought-Leader Series: Tim Ottinger  
> https://www.meetup.com/Chicago-Agile-Open-Space/events/236246295

--

### 21st

- I need a better way of following this habit.

--

### 28th

- Can't have a module and a class with the same name in Rails. #rails
	- But you can still include a class inside another class to get the same namespacing.

- This:

	```
	module FooModule
	  FOO = "it works"
	end
	
	class A
	  include FooModule
	
	  def foo
	    "#{FOO} in the outer class that includes it"
	  end
	
	  class B
	    def foo
	      begin
	        puts "when we try to access the constant from the inner class..."
	        FOO
	      rescue => e
	        puts e
	        "but #{A::FOO} namespaced to the outer class"
	      end
	    end
	  end
	end
	
	puts A.new.foo
	puts A::B.new.foo
	
	# Result
		it works in the outer class that includes it
		when we try to access the constant from the inner class...
		uninitialized constant A::B::FOO
		Did you mean?  FooModule
	               A::FOO
		but it works namespaced to the outer class
	```

- Empirical Software Engineering
	> https://modeling-languages.com/negative-results-empirical-software-engineering/

- COCOMO
	> https://en.wikipedia.org/wiki/COCOMO
	
-- 

### 29th

- Helm is a manifest manager thing for Kubernetes stuff. (Went to Docker/Kube/Helm meetup)

--

### 30th

- Branch.io links are reusa

Grab bag:

- Savepoints in Postgres
- `halt` in Sinatra: http://myronmars.to/n/dev-blog/2012/01/why-sinatras-halt-is-awesome
- What do the benchmark @cstime, @stime etc. things me

## December 2017

## January 2018

### 2nd

- Rails migration: Multiple `t.foreign_key :foo` statements in the same migration, to the same table, will overwrite one another. (As of Rails 4.2.5, [see source code](activerecord-4.2.5/lib/active_record/connection_adapters/abstract/schema_definitions.rb))
