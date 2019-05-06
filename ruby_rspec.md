# Ruby - Bootstrapping RSpec Test Suite

*__Note__: This guide assumes you have Ruby installed.*

1. Install Bundler

	```
	gem install bundler
	```

2. Create a new project folder for the code:

	(*Assuming project name is `new_kata`*)

	```
	mkdir new_kata
	cd new_kata
	```

3. In the new project folder, initialize the `Gemfile`

	```
	bundle init
	```

4. Install RSpec

	```
	bundle add rspec --group "test"
	```

5. Initialize an RSpec test suite

	```
	bundle exec rspec --init
	```

6. Create a test file (`spec/sum_spec.rb`) with the following content:

	```ruby
	require 'spec_helper'
	require_relative '../sum'

	describe 'sum' do
	  it 'adds 1 + 2 to equal 3' do
	    expect(sum(1, 2)).to eq 3
	  end
	end
	```

7. Create `sum.rb` with the following content:

	```ruby
	def sum(a, b)
	  a + b
	end
	```

8. Run the test

	```
	bundle exec rspec
	```

	You should see this:

	```
	.

	Finished in 0.00456 seconds (files took 0.10443 seconds to load)
	1 example, 0 failures
	```

9. Read up more about the types of test matchers available in RSpec: [https://relishapp.com/rspec/rspec-expectations/v/3-8/docs](https://relishapp.com/rspec/rspec-expectations/v/3-8/docs)