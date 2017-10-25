# learned-today
Just a readme. To log things I learn.

### October 2017

---

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