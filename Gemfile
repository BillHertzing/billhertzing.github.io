source "https://rubygems.org"
# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
gem "jekyll", "~> 4.2.0"
# This is the Minimal Mistakes theme.
gem "minimal-mistakes-jekyll", "~> 4.22.0"
# [jekyll-compose](https://github.com/jekyll/jekyll-compose) adds commands that help streamline the creation and publishing of posts
gem 'jekyll-compose', group: [:jekyll_plugins]
# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-paginate", "~> 1.1.0"
  gem "jekyll-sitemap", "~> 1.4.0"
  gem "jekyll-gist", "~> 1.5.0"
  gem "jekyll-feed", "~> 0.15.1"
  gem "jekyll-include-cache", "~> 0.2.1"
  gem "jekyll-timeago", "~> 0.14.0"
  gem "jekyll_version_plugin", "~> 2.0.0"
  # gem "jekyll-minifier", "~> 0.1.10"
  gem "jekyll-archives", "~> 2.2.1"
  gem "flexible_include", "~> 1.1.0"
  gem "jekyll-relative-links", "~> 0.6.1"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]


gem "webrick", "~> 1.7"
