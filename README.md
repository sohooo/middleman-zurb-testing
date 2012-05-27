Trying to run `middleman --pre` (3.0.0.beta.3) together with ZURBs Foundation. Problem: defining the gem `zurb-foundation` in the `Gemfile` seems to result in a massive cycle, due to the unmet/misspelt dependency `addresasble` (should be `addressable`).

## Versions

    # versions
    % bundle --version
    Bundler version 1.1.3

    % gem --version
    1.8.11


## bundle install

    # install gems in this project
    % bundle install --verbose
    Fetching gem metadata from http://rubygems.org/
    Query List: ["middleman", "zurb-foundation"]
    Query Gemcutter Dependency Endpoint API: middleman zurb-foundation
    Fetching from: http://rubygems.org/api/v1/dependencies?gems=middleman,zurb-foundation
    HTTP Success
    ...
    ...
    Unmet Dependencies: ["addresasble", "chriseppstein-compass", "jnunemaker-crack"]
    Fetching gem metadata from http://rubygems.org/
    Query List: ["addresasble", "chriseppstein-compass", "jnunemaker-crack"]
    Query Gemcutter Dependency Endpoint API: addresasble chriseppstein-compass jnunemaker-crack
    Fetching from: http://rubygems.org/api/v1/dependencies?gems=addresasble,chriseppstein-compass,jnunemaker-crack
    HTTP Success
    Query List: []

At this point, there's no response and everything hangs. Looking at the unmet dependencies, there seems to be a typo with `addressable` in the dependencies array above. `gem search -r addresasble` has no results.


## Abort stack trace


    ^C
    Quitting...
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/1.9.1/rubygems/requirement.rb:151:in `block in prerelease?'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/1.9.1/rubygems/requirement.rb:151:in `each'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/1.9.1/rubygems/requirement.rb:151:in `any?'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/1.9.1/rubygems/requirement.rb:151:in `prerelease?'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:178:in `block in resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:176:in `each'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:176:in `sort_by'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:176:in `resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:346:in `block in resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `catch'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:295:in `block in resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `reverse_each'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:346:in `block in resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `catch'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:295:in `block in resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `reverse_each'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:346:in `block in resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `catch'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:295:in `block in resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `reverse_each'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:294:in `resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:222:in `resolve'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:346:in `block in resolve_requirement'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `catch'
    /Users/soho/.rbenv/versions/1.9.3-p0/lib/ruby/gems/1.9.1/gems/bundler-1.1.3/lib/bundler/resolver.rb:344:in `resolve_requirement'
    ...
    ...


