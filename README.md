# PostgREST

## Status

[![Build Status](https://api.travis-ci.com/marcelobarreto/postgrest-rb.svg?branch=master)](https://travis-ci.com/marcelobarreto/postgrest-rb)
[![Code Climate](https://codeclimate.com/github/marcelobarreto/postgrest-rb.svg)](https://codeclimate.com/github/marcelobarreto/postgrest-rb)
[![Code Climate](https://codeclimate.com/github/marcelobarreto/postgrest-rb/coverage.svg)](https://codeclimate.com/github/marcelobarreto/postgrest-rb)
[![Ruby Style Guide](https://img.shields.io/badge/code_style-rubocop-brightgreen.svg)](https://github.com/rubocop/rubocop)
[![RubyGems](http://img.shields.io/gem/dt/postgrest.svg?style=flat)](http://rubygems.org/gems/postgrest)

Ruby client for [PostgREST](https://postgrest.org/)

This gem is under development, any help are welcome :muscle:

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'postgrest'
```

And then execute:

`$ bundle install`

Or install it yourself as:

`$ gem install postgrest`

## Usage

### Configuration

```ruby
db = Postgrest::Client.new(url: url, headers: headers, schema: schema)
```

### Selecting

```ruby
# Basic select

db.from('todos').select('*')

<Postgrest::Response:0x0000556745caa420
  @body={:select=>"*"},
  @count=1,
  @data=[{"id"=>1, "title"=>"Go to the gym", "completed"=>false}],
  @error=true,
  @status=200,
  @status_text="OK">

# Selecting just one or more fields

db.from('todos').select('title, completed')

<Postgrest::Response:0x0000556745590770
  @body={:select=>"title, completed"},
  @count=1,
  @data=[{"title"=>"Go to the gym", "completed"=>false}],
  @error=true,
  @status=200,
  @status_text="OK">

```

### Inserting

```ruby
db.from('todos').insert({ title: 'Go to the gym', completed: false })

<Postgrest::Response:0x00005567458aebf0 @body={:title=>"Go to the gym", :completed=>false}, @count=nil, @data="", @error=false, @status=201, @status_text="Created">

# Inserting multiple rows at once
db.from('todos').insert([
  { title: 'Go to the gym', completed: false },
  { title: 'Walk in the park', completed: true },
])

<Postgrest::Response:0x0000556745cdd118
  @body=[{:title=>"Go to the gym", :completed=>false}, {:title=>"Walk in the park", :completed=>true}],
  @count=nil,
  @data="",
  @error=true,
  @status=201,
  @status_text="Created">

```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/marcelobarreto/postgrest.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
