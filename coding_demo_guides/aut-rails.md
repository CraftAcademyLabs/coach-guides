gem install rails, but i dont need to do that

```
rails new rails_demo_cohort --database=postgresql --skip-test
```
 - cd into the application and open up in VS
 - aut : acceptance unit test
 
 ```
rails db:create
```
 
 **MAKE A COMMIT**

 - Open up the server to show the 'yay'!

 - go to gemfile and clean up - change byebug to pry-rails

 ```
group :development, :test do
  gem 'rspec-rails'
  gem 'shoulda-matchers'
  gem 'factory_bot_rails'
  gem 'capybara' 
  gem 'pry-rails'
end
 ```
- shoulda makes our unit tests shorter and easier
- capybara is the testing of the view layer easier to test

 - run bundle 

```
rails g 
```
- will show all the generators that we have available 
```
rails g rspec install
```

```
.rspec 

--format documentation
```
- put in spec_helper
```
require 'rails_helper'
```

```
# rails_helper

RSpec.configure do |config|
	config.fixture_path = "#{::Rails.root}/spec/fixtures"
	config.use_transactional_fixtures = true
	config.infer_spec_type_from_file_location!
	config.filter_rails_from_backtrace!
	config.include FactoryBot::Syntax::Methods
end

Shoulda::Matchers.configure do |config|
	config.integrate do |with|
		with.test_framework :rspec
		with.library :rails
	end
```
- run rspec 

**COMMIT**

```
config/application.rb 

config.generators do |generate|
		generate.helper false
		generate.assets false
		generate.view_specs false
		generate.helper_specs false
		generate.routing_specs false
		generate.controller_specs false
    generate.request_specs false
	end
```
- checkout a new branch

- create feature folder and specfile 

```
# spec/features/user_can_see_list_of_articles_spec.rb

feature 'List articles on index page' do
  context 'with articles in db' do
    before do
      visit root_path
    end

    it 'displays first article title' do
      expect(page).to have_content 'A breaking news item'
    end

    it 'displays second article title' do
      expect(page).to have_content 'Some really breaking action'
    end
  end
end 
```
- we should get an error undefined root_path
- minimum is a controller
```
rails g controller Articles index
```
- controllers are ALWAYS plural and models are ALWAYS singular, rails is sensitive for naming convention 
- explain the routes and delete what is in there
```
root controller: :articles, action: :index
```
Hard code the articles in the index.html file

- everything goes green, take a break and get back to it after lunch

_______

- ask what the problem is with the implementation code at the moment 
- why is it bad to have things hard coded?

- we want to bring the data from the db
- create factories

```
# spec/features/user_can_see_list_of_articles_spec.rb

feature 'List articles on index page' do
  context 'with articles in db' do
    before do
      create(:article, title: 'A breaking news item')
      create(:article, title: 'Some really breaking action')
      visit root_path
    end

    it 'displays first article title' do
      expect(page).to have_content 'A breaking news item'
    end

    it 'displays second article title' do
      expect(page).to have_content 'Some really breaking action'
    end
  end
end 
```

- test should fail
- now we need to move to the unit tests, AUT cycle
- what is the difference between unit test and acceptance test?
- the visual, that you can drive the car
- what you can't see, what happens under the hood
- we will create the model now

```
rails g model Article title:string
```
- we need to define the attribute we want with the datatype is should be
- created a shit load of files for us

```
# spec/models/article_spec.rb
RSpec.describe Article, type: :model do
  describe 'DB table' do
    it { is_expected.to have_db_column :title }
  end
  
  describe 'Validations' do
    it { is_expected.to validate_presence_of :title }
  end
  
  describe 'Factory' do
    it 'should have valid Factory' do
      expect(create(:article)).to be_valid
    end
  end
end
```
- try to run rspec, explain how the migrations work
 - rails db:migrate

- run rspec
- look the migration 
- factory
- we can use validations to make sure that things are saved in a format that we want to not fill out database with bullshit content 

- all tests should go green now

- now we are going to change our frontend so it fetches the data from the db 
- delete everything from the index.html

```
def index
  @articles = Article.all
end
```
- the view is always connected to an action in the specific controller 
- now we are writing ruby in html, that what erb helps us with!
- embedded ruby
```
index.html

@articles.each do

  <% @articles.each do |article| %>
    <h1>
       <%= article.title %><br />
    </h1>
  <% end %>

```
- everything goes green! 
- SHOW ME??
- nothing is there... WHY?

- alright lets go to the console and create them for real
- it is like irb or pry inside 
- we are using ruby to modify our database! that is pretty amazing guys, because we don't need to use SQL. 

- we need to have a description

**COMMIT**

```
# spec/features/user_can_see_specific_article_spec.rb

feature 'User can see specific article' do
  before do
    create(:article, title: 'A breaking news item', content: 'Some breaking action')
    
    visit root_path
    click_on 'A breaking news item'
  end

  context 'Article displays' do
    it 'title' do
      expect(page).to have_content 'A breaking news item'
    end

    it 'content' do
      expect(page).to have_content 'Some breaking action'
    end
  end
end
```
- here we use the capybara matchers, which are for testing the views 
- now we need to change our article model and add the content
- show schema and talk about that file 

```
rails g migration AddContentToArticle content:text
```
- strings in rails has a limitation, and therefor we can use text instead
- Why don't we just add it to the schema?
- why don't we just go into the previous migration and change that?

- run the migrations, and add the tests about the content to the model spec
- update the factory

```
  <% @articles.each do |article| %>
    <h1>
       <%= link_to article.title, article_path(article) %><br />
    </h1>
  <% end %>

```
- lets fix the problems with our routes 
```
resources :articles, only: [:show]
```
```
def show
  
end
```
- we need to fix the template for the view 
```
  def index 
    @article = Article.find(params[:id])
  end
```

```
<%= @article.title %>
<%= @article.content %>
```

- and Boom! Everything is green! 


-------

- branch off

```
user_can_write_an_article

feature 'Visitor can write articles' do
  before do
    visit root_path
    click_on 'Write Article'
    fill_in 'Title', with: 'It is almost friday'
    fill_in 'Content', with: 'That means it is almost weekend, and we have a graduation on saturday!'
    click_on 'Create Article'
  end
  describe 'Visitor can write a article' do
    it 'Visitor should see success message' do
      expect(page).to have_content 'Article was successfully created!'
    end
  end
end
```
```
index.html

<%= link_to 'Write Article', new_article_path %>
```
- run rspec
- go to routes and add new

```
articles_controller


def new
  @article = Article.new
end
```
```
new.html.erb

<%= form_with model: @article, local: true do |form| %>
  <%= form.label :title%>
  <%= form.text_field :title %>
  <%= form.label :content%>
  <%= form.text_field :content%>
  <%= form.submit 'Create Article'%>
<% end %>

```

- add create to routes
```
def create 
 @article = Article.create(params.require(:article).permit(:title, :content))
 if @article.persisted?
  redirect_to root_path notice: 'Article was successfully created'
  else 
  redirect_ to new_article_path, notice: 'Error, try again'
  end
end
```
- run rspec
- go to layout, that is a template that display every view that we render. A bit like out main component in the index.js in React.
```
<% if flash[:notice]%>
<%= flash[:notice]%>
<% end %>
```
- and everything is green! 
- Show it in the server 

```
feature 'User can' do
    context 'edit and article' do
        before do
            create(:article, title: 'Some crispy news', content: 'Some breaking action')
            visit root_path
            click_on 'Edit Article'
        end

        it 'User can edit the content' do
            fill_in 'Content', with: 'Cheez Doodles are now available with chocolate'
            click_on 'Update Article'
            expect(page).to have_content 'Cheez Doodles are now available with chocolate'
        end
    end
end
```
- in the show html
```
<%= link_to 'Edit Article', edit_article_path(article) %>
```
- go to routes and add edit

```
edit.html.erb

<%= form_with model: @article, local: true do |form| %>
  <%= form.label :title%>
  <%= form.text_field :title %>
  <%= form.label :content%>
  <%= form.text_field :content%>
  <%= form.submit 'Save Article'%>
<% end %>

```
- add edit to the controller

```
  @article = Article.find(params[:id])
```
- add update to routes
- add update to controllr

```
def update 
    @article = Article.find(params[:id])
    if @article.update(article_params)
      redirect_to @article notice: 'Article was successfully updated'
    else 
    redirect_ to edit_article_path, notice: 'Error, try again'
    end
  end
```





