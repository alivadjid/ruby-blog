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

`bin/rails db:migrate`
[Active_Record_Migrations](https://guides.rubyonrails.org/active_record_migrations.html)

6.3. Using a Model to Interact with the Database
`bin/rails console`
You should see an irb prompt like:
`Loading development environment (Rails 7.0.0) irb(main):001:0>`

new Article Object
`irb> article = Article.new(title: "Hello Rails", body: "I am on Rails!")`

`irb> article.save (0.1ms) begin transaction Article Create (0.4ms) INSERT INTO "articles" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?) [["title", "Hello Rails"], ["body", "I am on Rails!"], ["created_at", "2020-01-18 23:47:30.734416"], ["updated_at", "2020-01-18 23:47:30.734416"]] (0.9ms) commit transaction => true`

`Article.find(1)`
`Article.all`
This method returns an ActiveRecord::Relation object, which you can think of as a super-powered array.

[Active_Record_Basics](https://guides.rubyonrails.org/active_record_basics.html)
[Active_Record_Query_Interface](https://guides.rubyonrails.org/active_record_querying.html)

6.4. Showing a list of Articles
