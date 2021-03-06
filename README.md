#Ohana API

[![Build Status](https://travis-ci.org/codeforamerica/ohana-api.png?branch=master)](https://travis-ci.org/codeforamerica/ohana-api) [![Coverage Status](https://coveralls.io/repos/codeforamerica/ohana-api/badge.png?branch=master)](https://coveralls.io/r/codeforamerica/ohana-api) [![Dependency Status](https://gemnasium.com/codeforamerica/ohana-api.png)](https://gemnasium.com/codeforamerica/ohana-api)

A brand new project underway by Code for America's 2013 San Mateo County fellowship team. The goal is to build a read/write API for accessing data about available community social services.

This repo is in the early stages of development, stay tuned for when we are ready to accept contributions.

There is a front-end portion of this project under development at [Human Services Finder](https://github.com/codeforamerica/human_services_finder)

## Installation
Please note that the instructions below have only been tested on OS X. If you are running another operating system and run into any issues, feel free to update this README, or open an issue if you are unable to resolve installation issues.

###Prerequisites

#### Git, Ruby 2.0.0+, Rails 3.2.13+ (+ Homebrew on OS X)
**OS X**: [Set up a dev environment on OS X with Homebrew, Git, RVM, Ruby, and Rails](http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)

**Windows**: Try [RailsInstaller](http://railsinstaller.org), along with some of these [tutorials](https://www.google.com/search?q=install+rails+on+windows) if you get stuck.


#### MongoDB
**OS X**

On OS X, the easiest way to install MongoDB (or almost any development tool) is with Homebrew:

    brew update
    brew install mongodb

Follow the Homebrew instructions for configuring MongoDB and starting it automatically every time you restart your computer. Otherwise, you can launch MongoDB manually in a separate Terminal tab or window with this command:

    mongod

**Other**

See the Downloads page on mongodb.org for steps to install on other systems: [http://www.mongodb.org/downloads](http://www.mongodb.org/downloads)


#### Redis
**OS X**

On OS X, the easiest way to install Redis is with Homebrew:

    brew install redis

Follow the Homebrew instructions if you want Redis to start automatically every time you restart your computer. Otherwise launch Redis manually in a separate Terminal tab or window:

    redis-server

**Other**

See the Download page on Redis.io for steps to install on other systems: [http://redis.io/download](http://redis.io/download)

### Clone the app on your local machine:

    git clone git://github.com/codeforamerica/ohana-api.git
    cd ohana-api

### Install the dependencies:

    bundle

### Load the data
You can load a dataset of community-based organizations in San Mateo County in your local db with this command:

    rake load_data

Create the geospatial indexes for the [geocoder](https://github.com/alexreisner/geocoder) gem:

    rake db:mongoid:create_indexes

### Run the app
Start the app locally using Unicorn:

    unicorn

### Verify the app is returning JSON

    [http://localhost:8080/api/organizations](http://localhost:8080/api/organizations)

We recommend these tools to interact with APIs:

[JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) Chrome extension

[HTTPie](https://github.com/jkbr/httpie) command line utility

### API documentation (work in progress)
[http://docs.ohanapi.apiary.io/](http://docs.ohanapi.apiary.io/)


### User authentication and emails
The app allows developers to sign up for an account, but all email addresses need to be verified first. In development, the app sends email via Gmail. If you want to try this email process on your local machine, you need to configure your Gmail username and password by creating a file called `application.yml` in the config folder, and entering your info like so:

    GMAIL_USERNAME: your_email@gmail.com
    GMAIL_PASSWORD: your_password

`application.yml` is ignored in `.gitignore`, so you don't have to worry about exposing your credentials if you ever push code to GitHub. If you don't care about email interactions, but still want to try out the signed in experience, you can load 2 example users in the database with this command:

    rake db:seed

You can then [sign in](http://localhost:8080/users/sign_in) with either of those users, whose username and password are stored in `db/seeds.rb`.


## Development Details

* Ruby version 2.0.0
* Rails version 3.2.13
* MongoDB with the Mongoid ORM
* Template Engines: ERB and HAML
* Testing Frameworks: RSpec, Factory Girl
* Redis

## Contributing

In the spirit of open source software, **everyone** is encouraged to help improve this project.

Here are some ways *you* can contribute:

* by using alpha, beta, and prerelease versions
* by reporting bugs
* by suggesting new features
* by suggesting labels for our issues
* by writing or editing documentation
* by writing specifications
* by writing code (**no patch is too small**: fix typos, add comments, clean up
  inconsistent whitespace)
* by refactoring code
* by closing [issues](https://github.com/codeforamerica/ohana-api/issues)
* by reviewing patches
* [financially](https://secure.codeforamerica.org/page/contribute)

## Submitting an Issue
We use the [GitHub issue tracker](https://github.com/codeforamerica/ohana-api/issues) to track bugs and features. Before submitting a bug report or feature request, check to make sure it hasn't already been submitted. When submitting a bug report, please include a [Gist](https://gist.github.com/) that includes a stack trace and any details that may be necessary to reproduce the bug, including your gem version, Ruby version, and operating system. Ideally, a bug report should include a pull request with failing specs.

## Submitting a Pull Request
1. [Fork the repository.][fork]
2. [Create a topic branch.][branch]
3. Add specs for your unimplemented feature or bug fix.
4. Run `rspec`. If your specs pass, return to step 3. In the spirit of Test-Driven Development, you want to write a failing test first, then implement the feature or bug fix to make the test pass.
5. Implement your feature or bug fix.
6. Run `rspec`. If your specs fail, return to step 5.
7. Run `metric_fu -r`. This will go through all the files in the app and analyze the code quality and check for things like trailing whitespaces and hard tabs. When it's done, it will open a page in your browser with the results. Click on `Cane` and `Rails Best Practices` to check for files containing trailing whitespaces and hard tabs. If you use Sublime Text 2, you can use the [TrailingSpaces](https://github.com/SublimeText/TrailingSpaces) plugin to highlight the trailing whitespaces and delete them. If the report complains about "hard tabs" in a file, change your indentation to `spaces` by clicking on `Tabs: 2` at the bottom of your Sublime Text 2 window, then selecting `Convert Indentation to Spaces`. As for the code itself, we try to follow [GitHub's Ruby styleguide](https://github.com/styleguide/ruby).
8. Add, commit, and push your changes.
9. [Submit a pull request.][pr]

[fork]: http://help.github.com/fork-a-repo/
[branch]: http://learn.github.com/p/branching.html
[pr]: http://help.github.com/send-pull-requests/

## Copyright
Copyright (c) 2013 Code for America. See [LICENSE](https://github.com/codeforamerica/ohana-api/blob/master/LICENSE.md) for details.