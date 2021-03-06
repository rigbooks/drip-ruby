# Drip Ruby Bindings

A Ruby toolkit for the [Drip](https://www.getdrip.com/) API.

## Installation

Add this line to your application's Gemfile:

    gem 'drip-ruby', :require => 'drip'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install drip-ruby

## Usage

Your account ID can be found [here](https://www.getdrip.com/settings/site).

For private integrations, you may use your personal API key (found
[here](https://www.getdrip.com/user/edit)) via the `api_key` setting:

```ruby
client = Drip::Client.new do |c|
  c.api_key = "YOUR_API_KEY"
  c.account_id = "YOUR_ACCOUNT_ID"
end
```

For public integrations, pass in the user's OAuth token via the `access_token`
setting:

```ruby
client = Drip::Client.new do |c|
  c.access_token = "YOUR_ACCESS_TOKEN"
  c.account_id = "YOUR_ACCOUNT_ID"
end
```

Since the Drip client is a flat API client, most API actions are available
as methods on the client object. The following methods are currently available:

| Action                     | Method                                               |
| :------------------------- | :--------------------------------------------------- |
| Create/update a subscriber | `#create_or_update_subscriber(email, options = {})`  |
| Create/update a batch of subscribers | `#create_or_update_subscribers(subscribers)` |
| Fetch a subscriber         | `#subscriber(id_or_email)`                           |
| Subscribe to a campaign    | `#subscribe(email, campaign_id, options = {})`       |
| Unsubscribe                | `#unsubscribe(id_or_email, options = {})`            |
| Apply a tag                | `#apply_tag(email, tag)`                             |
| Remove a tag               | `#remove_tag(email, tag)`                            |
| Track an event             | `#track_event(email, action, properties = {})`       |
| Track a batch of events    | `#track_events(events)`                              |


**Note:** We do not have complete API coverage yet. If we are missing an API method
that you need to use in your application, please file an issue and/or open a
pull request. [See the official REST API docs](https://www.getdrip.com/docs/rest-api)
for a complete API reference.

## Examples

```ruby
client = Drip::Client.new do |c|
  c.api_key = "YOUR_API_TOKEN"
  c.account_id = "YOUR_ACCOUNT_ID"
end

# Fetch a subscriber
resp = client.subscriber("foo@example.com")
# => <Drip::Response ...>

resp.success?
# => true

subscriber = resp.subscribers.first
subscriber.email
# => "foo@example.com"
```

## Contributing

1. Fork it ( https://github.com/DripEmail/drip-ruby/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
