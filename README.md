# learned-today
Just a readme. To log things I learn.

## 2017
### October
----
---- 24th ----

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
	
- The body of a GET request is semantically meaningless. #http
	- https://stackoverflow.com/questions/978061/http-get-with-request-body

#### 25th