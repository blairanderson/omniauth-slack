# Omniauth::Slack

This Gem contains the Slack strategy for OmniAuth.

## Before You Begin

You should have already installed OmniAuth into your app; if not, read the [OmniAuth README](https://github.com/intridea/omniauth) to get started.


Now sign into the [Slack application dashboard](https://api.slack.com/applications) and create an application. Take note of your API keys.


## Using This Strategy

First start by adding this gem to your Gemfile:

```ruby
gem 'omniauth-slack'
```

If you need to use the latest HEAD version, you can do so with:

```ruby
gem 'omniauth-slack', github: 'kmrshntr/omniauth-slack'
```

Next, tell OmniAuth about this provider. For a Rails app, your `config/initializers/omniauth.rb` file should look like this:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :slack, "API_KEY", "API_SECRET", scope: "client"
end
```

Replace `"API_KEY"` and `"API_SECRET"` with the appropriate values you obtained [earlier](https://api.slack.com/applications).

If you are using [Devise](https://github.com/plataformatec/devise) then it will look like this:

```ruby
Devise.setup do |config|
  # other stuff...

  config.omniauth :slack, ENV["SLACK_APP_ID"], ENV["SLACK_APP_SECRET"], scope: 'client'

  # other stuff...
end
```

Slack lets you choose from a [few different scopes](https://api.slack.com/docs/oauth#auth_scopes).


## Authentication Options

#### State

> *unique string to be passed back upon completion*

> The state parameter should be used to avoid forgery attacks by passing in a value that's unique to the user you're authenticating and checking it when auth completes.

for a logged in user, you might want to include state, for example with devise:

`https://www.yourapp.com/users/auth/slack?state=1234-foobutter`

creates an auth session with `state`

After a successful auth, the callback request will include `request.env["omniauth.params"]` hash

```ruby
class CallbackController < ApplicationController
  def slack
    request.env["omniauth.params"]["state"]
    # => "1234-foobutter"
  end
end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/kmrshntr/omniauth-slack/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

