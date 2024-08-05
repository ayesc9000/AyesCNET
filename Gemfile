source "https://rubygems.org"

# NOTES:
# Minima was removed because it is not used at all throughout the site.
# WDM was removed because it is broken and does not compile.

# Last tested against Jekyll 4.3.3
gem "jekyll", "~> 4.3.3"

# Put Jekyll plugins in this group
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]

# Rouge is our code syntax highligher.
gem 'rouge', '~> 4.3'

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of
# the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]

# CSV is no longer part of the standard library as of Ruby 3.4.0 and Jekyll has
# not yet included it in their gemfile.
gem 'csv', '~> 3.3'

# Base64 is no longer part of the standard library as of Ruby 3.4.0 and Safe Yaml
# has not yet included it in their gemfile.
gem 'base64', '~> 0.2.0'
