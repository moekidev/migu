# Migu

Migu is a migration tool for vector databases that lack a well-established migration mechanism. It is implemented as a Ruby code base.

## Installation

Install the gem and add to the application's Gemfile by executing:

    $ bundle add migu

If bundler is not being used to manage dependencies, install the gem by executing:

    $ gem install migu

## Usage

```
$ migu help
Commands:
  migu generate NAME           # Generate migration file to migu/migrate/ directory
  migu init                    # Initialize Migu SQLite3 database. migu/state.sqlite3 will be created.
  migu ls                      # List migrations
  migu migrate                 # Migrate all migrations
  migu reset                   # Migu Reset
  migu rollback                # Rollback 1 migration
  migu version                 # Print version
```

### Init

Initialize Migu SQLite3 databse for managing migration states.

```
migu init
```

This command will create `migu/state.sqlite3`.

### Generate

Generate migration file to `migu/migrate/**.rb`.

```
migu generate create_users
```

### Define migration class

Example:

```ruby
class CreateUsers < Migu::Migration
  def self.time
    "2023-06-30 23:27:50 +0900" # Do not edit
  end

  def up
    client = Weaviate::Client.new
    client.schema.create(
      # ...
    )
  end

  def down
    client.schema.delete(
      # ...
    )
  end
end
```

### Migrate

```
migu migrate
```

### Rollback

```
migu rollback
```

### List

```bash
$ migu ls
bundle exec migu ls
CreateUsers migrated
CreatePosts not_migrated
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and the created tag, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/moekidev/migu. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/moekidev/migu/blob/main/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the migu project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/moekidev/migu/blob/main/CODE_OF_CONDUCT.md).
