Spagetti Car is a test Vanilla Install of Solidus




# Solidus

[![Circle CI](https://circleci.com/gh/solidusio/solidus/tree/master.svg?style=shield)](https://circleci.com/gh/solidusio/solidus/tree/master)
[![Gem](https://img.shields.io/gem/v/solidus.svg)](https://rubygems.org/gems/solidus)
[![License](http://img.shields.io/badge/license-BSD-yellowgreen.svg)](LICENSE.md)
[![Reviewed by Hound](https://img.shields.io/badge/Reviewed_by-Hound-8E64B0.svg)](https://houndci.com)

[![Enthusiasts on Open Collective](https://opencollective.com/solidus/tiers/enthusiast/badge.svg?label=Enthusiasts&color=brightgree)](https://opencollective.com/solidus)
[![Supporters on Open Collective](https://opencollective.com/solidus/tiers/supporter/badge.svg?label=Supporters&color=brightgree)](https://opencollective.com/solidus)
[![Ambassadors on Open Collective](https://opencollective.com/solidus/tiers/ambassador/badge.svg?label=Ambassador&color=brightgree)](https://opencollective.com/solidus)
[![Open Source Helpers](https://www.codetriage.com/solidusio/solidus/badges/users.svg)](https://www.codetriage.com/solidusio/solidus)
[![Slack](http://slack.solidus.io/badge.svg)](http://slack.solidus.io)




## Table of Contents
- [Supporting Solidus](#supporting-solidus)
- [Summary](#summary)
- [Demo](#demo)
- [Getting Started](#getting-started)
- [Installation Options](#installation-options)
- [Performance](#performance)
- [Developing Solidus](#developing-solidus)
- [Contributing](#contributing)




---

## Summary

Solidus is a complete open source ecommerce solution built with Ruby on Rails.
It is a fork of [Spree](https://spreecommerce.org).

See the [Solidus class documentation](http://docs.solidus.io) and the [Solidus
Guides](https://guides.solidus.io) for information about the functionality that
Solidus provides.

Solidus consists of several gems. When you require the `solidus` gem in your
`Gemfile`, Bundler will install all of the gems maintained in this repository:

- [`solidus_api`](https://github.com/solidusio/solidus/tree/master/api) (RESTful API)
- [`solidus_frontend`](https://github.com/solidusio/solidus/tree/master/frontend) (Cart and storefront)
- [`solidus_backend`](https://github.com/solidusio/solidus/tree/master/backend) (Admin area)
- [`solidus_core`](https://github.com/solidusio/solidus/tree/master/core) (Essential models, mailers, and classes)
- [`solidus_sample`](https://github.com/solidusio/solidus/tree/master/sample) (Sample data)

All of the gems are designed to work together to provide a fully functional
ecommerce platform. However, you may only want to use the
[`solidus_core`](https://github.com/solidusio/solidus/tree/master/core) gem
combine it with your own custom frontend, admin interface, and API.


## Developing Solidus

* Clone the Git repo

  ```bash
  git clone git://github.com/solidusio/solidus.git
  cd solidus
  ```

* Install the gem dependencies

  ```bash
  bin/setup
  ```

  _Note_: If you're using PostgreSQL or MySQL, you'll need to install those gems through the DB environment variable.

  ```bash
  # PostgreSQL
  export DB=postgresql
  bin/setup

  # MySQL
  export DB=mysql
  bin/setup
  ```

### Sandbox

Solidus is meant to be run within the context of Rails application. You can
easily create a sandbox application inside of your cloned source directory for
testing purposes.

This sandbox includes solidus\_auth\_devise and generates with seed and sample
data already loaded.

* Create the sandbox application

  ```bash
  bin/sandbox
  ```

  You can create a sandbox with PostgreSQL or MySQL by setting the DB environment variable.

  ```bash
  # PostgreSQL
  export DB=postgresql
  bin/sandbox

  # MySQL
  export DB=mysql
  bin/sandbox
  ```

  If you need to create a Rails 5.2 application for your sandbox, for example
  if you are still using Ruby 2.4 which is not supported by Rails 6, you can
  use the `RAILS_VERSION` environment variable.

  ```bash
    export RAILS_VERSION='~> 5.2.0'
    bin/setup
    bin/sandbox
  ```

* Start the server (`bin/rails` will forward any argument to the sandbox)

  ```bash
  bin/rails server
  ```

### Tests

Solidus uses [RSpec](http://rspec.info) for tests. Refer to its documentation for
more information about the testing library.

#### CircleCI

We use CircleCI to run the tests for Solidus as well as all incoming pull
requests. All pull requests must pass to be merged.

You can see the build statuses at
[https://circleci.com/gh/solidusio/solidus](https://circleci.com/gh/solidusio/solidus).

#### Run all tests

[ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/home) is
required to run the frontend and backend test suites.

To execute all of the test specs, run the `bin/build` script at the root of the Solidus project:

```bash
createuser --superuser --echo postgres # only the first time
bin/build
```

The `bin/build` script runs using PostgreSQL by default, but it can be overridden by setting the DB environment variable to `DB=sqlite` or `DB=mysql`. For example:

```bash
env DB=mysql bin/build
```

If the command fails with MySQL related errors you can try creating a user with this command:

```bash
# Creates a user with the same name as the current user and no restrictions.
mysql --user="root" --execute="CREATE USER '$USER'@'localhost'; GRANT ALL PRIVILEGES ON * . * TO '$USER'@'localhost';"
```

#### Run an individual test suite

Each gem contains its own series of tests. To run the tests for the core project:

```bash
cd core
bundle exec rspec
```

By default, `rspec` runs the tests for SQLite 3. If you would like to run specs
against another database you may specify the database in the command:

```bash
env DB=postgresql bundle exec rspec
```

#### Code coverage reports

If you want to run the [SimpleCov](https://github.com/colszowka/simplecov) code
coverage report:

```bash
COVERAGE=true bundle exec rspec
```

### Extensions

In addition to core functionality provided in Solidus, there are a number of
ways to add features to your store that are not (or not yet) part of the core
project.

A list can be found at [extensions.solidus.io](http://extensions.solidus.io/).

If you want to write an extension for Solidus, you can use the
[solidus_dev_support](https://github.com/solidusio/solidus_dev_support.git) gem.

