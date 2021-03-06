[![Gem Version](https://badge.fury.io/rb/rails_admin_google_map.svg)](https://badge.fury.io/rb/rails_admin_google_map)

# RailsAdminGoogleMap
Implementation of user friendly google map field in rails_admin.
Any suggestions are welcome.

![Example](http://i.imgur.com/ZlxMvZK.png)

## TODO
- [ ] Test with multiple google map field within the same model
- [ ] More Google map options

## Installation
Add this line to your application's Gemfile:

```ruby
gem 'rails_admin_google_map'
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install rails_admin_google_map
```

## Usage
Strategy: using a serialized field to store all google map data. We store all datas return

### Migration example:
```ruby
def change
  add_column :users, :google_map, :text
end
```

#### In your model:
```ruby
class User < ActiveRecord::Base
  serialize :google_map, JSON
end
```

#### RailsAdmin configuration
```ruby
RailsAdmin.config do |config|
  config.model Point do
    edit do
      field :google_map, :google_map do
        google_api_key 'APIKEY'
        default_latitude -34.0
        default_longitude 151.0
        locale 'en'
      end
    end
  end
end
```

Example of JSON stored values, everything is build dynamically and depends on Google return.

```javascript
{
  "location":{
      "latitude":45.5016889,
      "longitude":-73.56725599999999
   },
   "formatted_address":"Montréal, QC, Canada",
   "locality":"Montréal",
   "political":"Canada",
   "administrative_area_level_3":"Pointe-Calumet",
   "administrative_area_level_2":"Communauté-Urbaine-de-Montréal",
   "administrative_area_level_1":"Québec",
   "country":"Canada"
}
```

Example of usage in a view

```
<%= u.google_map['location']['latitude'] %>
<%= u.google_map['country'] %>
<%= u.google_map['formatted_address'] %>
```

## License
The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
