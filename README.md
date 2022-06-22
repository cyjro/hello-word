# hello-word
Just another repository
name: My workflow
on: [push, pull_request]
jobs:
  test:
    strategy:
      fail-fast: false
      matrix:
        gemfile: [ rails5, rails6 ]
    runs-on: ubuntu-latest
    env: # $BUNDLE_GEMFILE must be set at the job level, so it is set for all steps
      BUNDLE_GEMFILE: ${{ github.workspace }}/gemfiles/${{ matrix.gemfile }}.gemfile
    steps:
      - uses: actions/checkout@v3
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.0'
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically
      - run: bundle exec rake
