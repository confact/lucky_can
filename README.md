# lucky_can

An little nicer way to handle authorization rules for your lucky app

## Installation

1. Add the dependency to your `shard.yml`:

   ```yaml
   dependencies:
     lucky_can:
       github: confact/lucky_can
   ```

2. Run `shards install`

## Usage

1. ```crystal
    require "lucky_can"
   ```

2. create an `policies` directory where all your policies will be. Now you will Add an require for that directory to the app.cr file before `pages` require. Add this: `require "./policies/**"`

3. now you can create your policies in `policies` directory.


### Simple usage

```crystal
class TeamPolicy < LuckyCan::BasePolicy
  can show, team, current_user do
    return false if current_user.nil?
    team.users.include?(current_user)
  end
end
```

this generate following methods for you to use by an macro:
* `TeamPolicy.show?(team, current_user)` - for simple bool check if the user have access to the team.
* `TeamPolicy.show_not_found?(team, current_user, context)` - Return an Lucky::RouteNotFoundError if the code in the block return false.
* `TeamPolicy.show_forbidden?(team, current_user, context)` - Return an LuckyCan::ForbiddenError if the code in the block return false.

## Contributing

1. Fork it (<https://github.com/confact/lucky_can/fork>)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## Contributors

- [Håkan Nylén](https://github.com/confact) - creator and maintainer
