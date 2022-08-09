# README

[RubyonRails](https://guides.rubyonrails.org/getting_started.html)

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

```
<% %> and <%= %>. The <% %> tag means "evaluate the enclosed Ruby code." The <%= %> tag means "evaluate the enclosed Ruby code, and output the value it returns."
```

We can see the final result by visiting http://localhost:3000. (Remember that bin/rails server must be running!) Here's what happens when we do that:

1 - The browser makes a request: GET http://localhost:3000.
2 - Our Rails application receives this request.
3 - The Rails router maps the root route to the index action of ArticlesController.
4 - The index action uses the Article model to fetch all articles in the database.
5 - Rails automatically renders the app/views/articles/index.html.erb view.
6 - The ERB code in the view is evaluated to output HTML.
7 - The server sends a response containing the HTML back to the browser.
We've connected all the MVC pieces together, and we have our first controller action! Next, we'll move on to the second action.

7.2. Resourceful Routing

Rails provides a routes method named resources that maps all of the conventional routes for a collection of resources, such as articles.

`bin/rails routes`

\_url or \_path form the names of these helpers. For example, the article_path helper returns "/articles/#{article.id}"

[Rails Routing from the Outside in](https://guides.rubyonrails.org/routing.html)

7.3. Creating a New Article

7.3.1 Using a Form Builder
form builder

[Action View Form Helpers](https://guides.rubyonrails.org/form_helpers.html)

7.3.2 Using Strong Parameters
[Action Controller Overview And Strong Parameters](https://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)

### 7.3.3. Validations and Displaying Error Messages

#### Feature. Disable keys updated_at, created_at and more in API

#### Удалить поля связанные с ДБ и АПИ

#### отправка запросов с postman. Например для создания формы

#### Авторизация

Валидация добавляется в модели

[Active Record Validations](https://guides.rubyonrails.org/active_record_validations.html#working-with-validation-errors)

### 7.3.4 Finishing up

### 7.4 Updating an Article

#### 7.4.1 Using Partials to Share VIew Code

Форма заменяется на общий код - \_form.html.erb

[Partials](https://guides.rubyonrails.org/layouts_and_rendering.html#using-partials)

#### 7.4.2 Finishing up

`redirect_to root_path, status: :see_other` - указывает на статус. Здесь будет 303 - see other
или `articles_path`

для удаления и подтверждения удаления используется [Turbo](https://turbo.hotwired.dev/)

### 7.5 Deleting an Article

## 8 Adding a Second Model

Добавление комментариев для articles

`bin/rails generate model Comment commenter:string body:text article:references `

Создалась модел Comment

```
  invoke  active_record
  create    db/migrate/20220802180544_create_comments.rb
  create    app/models/comment.rb
  invoke    test_unit
  create      test/models/comment_test.rb
  create      test/fixtures/comments.yml

```

`bin/rails db:migrate`

### 8.2 Associationg Models

Each comment belongs to one article.
One article can have many comments.

articles.rb has_many :comments
теперь в @artile будет @article.comments

[Active Record associations](https://guides.rubyonrails.org/association_basics.html)

### 8.3 Adding a Route for Comments

```
resources :articles do
resources :comments
end
```

Это создает комментарии как вложенный ресурс в статьях. Это еще одна часть фиксации иерархических отношений между статьями и комментариями.

[Rails Routing Guide](https://guides.rubyonrails.org/routing.html)

### 8.4 Generating a controller

`bin/rails generate controller Comments`

## 9 Refactoring

добавляем partial. \_comment.html.erb
`<%= render @article.comments %>`
каждый коммент рендерит с использованием partial - `_comment.html.erb`

### 9.2 Rendering a Partial Form

partial_form in `app/views/comments/_form.html.erb`

### 9.3 Using concerns

mixins

```
app/controllers/concerns
app/models/concerns

```

```
bin/rails generate migration AddStatusToArticles status:string
bin/rails generate migration AddStatusToComments status:string

```

```
bin/rails db:migrate

```

добавление поля status в комментарии и артикл

добавление в модели

view вывод не архивных данных

создаем модуль в models/concerns для валидных статусов
общий валид

Методы класса также могут быть добавлены к «проблемам». Если мы хотим отобразить количество общедоступных статей или комментариев на нашей главной странице, мы можем добавить метод класса к Visible следующим образом:

подсчет кол-ва не архивных комментов

добавление селекта статус в формы

## 10. Deleting comments

### 10.1 deleting associated object

if you delete an article, its associated comments will also need to be deleted
`has_many :comments, dependent: :destroy`
