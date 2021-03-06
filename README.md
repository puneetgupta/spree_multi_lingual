# SpreeMultiLingual [![Build Status](https://secure.travis-ci.org/jipiboily/spree_multi_lingual.png?branch=master)](http://travis-ci.org/jipiboily/spree_multi_lingual)

SpreeMultiLingual is originally a proof of concept for what could become a multi-lingual Spree plugin.

Since then integration tests and features have been added.

## Requirements
 - Spree 2.0.X
 - Rails 3.2.14


## Installation
Add gem to your Gemfile:

	gem 'spree_multi_lingual', :github => 'puneetgupta/spree_multi_lingual'
	gem 'easy_globalize3_accessors', :git => "git://github.com/reinkcar/easy_globalize3_accessors.git"
	gem 'globalize', '3.0.4'

Globalize3 edge version fixed important bug with dynamic finder : https://github.com/svenfuchs/globalize3/commit/b771fb87d3dda4a78cfe294da1fab7df266e72c9

Run Bundler

	bundle install

**Assets**

In app/assets/javascripts/admin/all.js

	//= require admin/spree_multi_lingual
	//= require admin/spree_multi_lingual_class

This is required for the language dropdown!


Add an initializer file and set SpreeMultiLingual.languages to an array containing the languages you support.

```ruby
# config/initializers/spree_multi_lingual.rb
SpreeMultiLingual.languages = ["fr", "en", "es"] # Add your own locales here
```

For the moment, enable locale fallbacks for i18n (makes lookups for any locale fall back to the i18n.default_locale when a translation can not be found)

```ruby
# config/application.rb
config.i18n.fallbacks = true
```

Run spree_multi_lingual install:

	rails g spree_multi_lingual:install

If you want to use browser language detection using rack-contrib Locale :

```ruby
# config.ru
require 'rack'
require 'rack/contrib'

use Rack::Locale

require ::File.expand_path('../config/environment',  __FILE__)
run MyRailsApp::Application
```

## Use
On views where there is translated fields, there should be a dropdown to switch currently edited locale.

Products:
http://dl.dropbox.com/u/6210261/spree_multi_lingual.swf

Taxons:
** /!\ Using the taxonomy tree you can only edit another locale taxons name, to do so click on the links next to "Edit Taxonomy" to show the taxonomy for a given locale.
If you want to create taxons using the taxonomy tree, please only use the default locale for the moment.**

To edit taxons permalink please do as following:
![Taxon](https://dl.dropbox.com/u/51922297/Screen%20Shot%202013-03-30%20at%201.03.00%20AM.png)
![TaxonEdit](https://dl.dropbox.com/u/51922297/Screen%20Shot%202013-03-30%20at%201.06.51%20AM.png)

### What is translated?

For now :
- products : name, permalink, description, meta description and meta keywords.
- taxonomies : name.
- taxons : name, permalink and description.

# WARNING
there is no fallback of default language for now unless you speficy i18n.fallbacks as previously stated.

## Notes

It uses Globalize3, easy_globalize3_accessors and routing-filter. Thanks to [Tomash](https://github.com/tomash) that told me about those two awesome gems: easy_globalize3_accessors and routing-filter.

SpreeMultiLingual depends on a fork of routing-filter because it supports :exclude option in routes, used for /admin. I hope it this feature can me merged into the original repo.

The flags are from the flags icon set from famfamfam (http://www.famfamfam.com/).

## TODO

1. Make taxons multi languages editable from the taxonomy tree
2. Dynamically show taxon prefix permalink depending on dropdown language selected : Taxons#edit
3. Add things to translate:
	- Option values
	- Properties
	- Alt text on images
4. Dropdown or something to change locale
5. Rake task for store that already have users

## Contributors

Special thanks to sbounmy for the amount of contributions he did. Thanks to Radar for merging spree_localize.

## Testing

Be sure to bundle your dependencies and then create a dummy test app for the specs to run against.

    $ bundle
    $ bundle exec rake test_app
    $ bundle exec rspec spec

Copyright (c) 2012 Jean-Philippe Boily, released under the New BSD License


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/jipiboily/spree_multi_lingual/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

