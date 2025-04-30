# AyesCNET
# Copyright (C) 2025  Liam "AyesC" Hogan
# 
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License along
# with this program; if not, write to the Free Software Foundation, Inc.,
# 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

source "https://rubygems.org"

# This is a modified version of the default Jekyll gemfile.

# Last tested against Jekyll 4.3.3.
gem "jekyll", "~> 4.3.3"

# Rouge is our code syntax highlighter.
gem 'rouge', '~> 4.3'

# Put Jekyll plugins in this group
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-toc", "~> 0.19.0"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of
# the gem do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]

# CSV is no longer part of the standard library as of Ruby 3.4.0 and Jekyll has
# not yet included it in their gemfile.
gem 'csv', '~> 3.3'

# Base64 is no longer part of the standard library as of Ruby 3.4.0 and Safe Yaml
# has not yet included it in their gemfile.
gem 'base64', '~> 0.2.0'
