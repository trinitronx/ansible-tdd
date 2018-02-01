source 'https://rubygems.org'

group :development do
#  gem 'ruby_gntp' ## Potentially all platforms? (Untested)

  case RUBY_PLATFORM
  when /darwin/
    gem 'terminal-notifier-guard'
    gem 'growl'
  when /linux/
    gem 'libnotify'
  when /win32/
    gem 'rb-notifu'
  end

  gem 'rb-fsevent'
  gem 'guard', '~> 1.8'
  gem 'guard-yaml'
  gem 'guard-shell'
  gem 'yaml-lint'
end
