Illustration of Issue with pry-byebug
================

Summary: when pry-byebug is added to this project's gem file and used during feature test (RSpec or Cucumber with Capybara) execution, the web thread/process waits on a `binding.pry` even if that breakpoint is located in the test file. When pry-byebug is removed, the web thread/process is not blocked and the user may click around around if they are using a non-headless browser (Selenium w/ Firefox in this case). 

### Steps to Reproduce
1. Clone this repo.
2. `bundle`
3. `rake db:create`
4. `rspec spec/features/users/sign_in_spec.rb:11`
5. When the break point is reached, attempt to click a link to a new page.

#### Expected Result
The server is able to handle the request and renders the page.

#### Actual Result
The server hangs waiting on the binding.pry call.

6. Continue on from the breakpoint. 
7. Remove `gem 'pry-byebug'` from the gem file.
8. `rspec spec/features/users/sign_in_spec.rb:11`
9. When the break point is reached, attempt to click a link to a new page.

#### Actual Result
The server does not wait on the binding.pry call.

-----------
