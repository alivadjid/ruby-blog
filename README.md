# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

- Ruby version

- System dependencies

- Configuration

- Database creation

- Database initialization

- How to run the test suite

- Services (job queues, cache servers, search engines, etc.)

- Deployment instructions

- ...

1. `rails new blog`

   4.2 Hello Rails
   routes.rb
   change route
   `bin/rails generate controller Articles index --skip-routes`

for next [link](https://guides.rubyonrails.org/autoloading_and_reloading_constants.html)

you only need require calls for two use cases:

- To load files under the lib directory.
- To load gem dependencies that have `require: false` in the Gemfile.

  6.1 Generating a Model.

`bin/rails generate model Article title:string body:text`
