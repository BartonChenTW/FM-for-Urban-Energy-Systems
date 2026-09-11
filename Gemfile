source "https://rubygems.org"

# GitHub Pages builds this site with its own pinned dependency set, so
# `github-pages` is the only Jekyll gem declared here -- it pins an exact
# version of Jekyll and of every plugin it bundles.
#
# Do NOT add `gem "just-the-docs"` here. The theme is pulled at build time
# via `remote_theme: just-the-docs/just-the-docs` in _config.yml, not from
# a gem, so the gem isn't needed -- and declaring it directly lets Bundler
# resolve a version that `github-pages` refuses, which fails the Pages
# build with "The github-pages gem can't satisfy your Gemfile's
# dependencies."
#
# Same applies to jekyll itself and to the plugins listed under `plugins:`
# in _config.yml (jekyll-remote-theme, jekyll-redirect-from): they all ship
# inside `github-pages` already.
gem "github-pages", group: :jekyll_plugins

# Only needed to run `bundle exec jekyll serve` locally on Ruby 3+, where
# webrick is no longer part of the standard library. Not used by the
# GitHub Pages build.
gem "webrick"
