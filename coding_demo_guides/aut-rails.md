gem install rails, but i dont need to do that

```
rails new rails_demo_cohort --api --database=postgresql --skip-test 
```
 - we need to pass in the api flag since rails can be used a fullstack application as well
 - cd into the application and open up in VS
 - aut : acceptance unit test
 
 ```
rails db:create db:migrate
```
 
 **MAKE A COMMIT**

 - Open up the server to show the 'yay'!

 - go to gemfile and clean up - change byebug to pry-rails

 ```
group :development, :test do
  gem 'rspec-rails'
  gem 'shoulda-matchers'
  gem 'factory_bot_rails'
  gem 'pry-rails'
end
 ```
- shoulda makes our unit tests shorter and easier

 - run bundle 

```
rails g 
```
- will show all the generators that we have available 
```
rails g rspec:install
```

```
.rspec 

--format documentation
--color
--require rails_helper
```

```
# rails_helper

Dir[Rails.root.join('spec/support/**/*.rb')].sort.each { |f| require f }

RSpec.configure do |config|
	config.fixture_path = "#{::Rails.root}/spec/fixtures"
	config.use_transactional_fixtures = true
	config.infer_spec_type_from_file_location!
	config.filter_rails_from_backtrace!
	config.include FactoryBot::Syntax::Methods
  config.include Shoulda::Matchers::ActiveRecord, type: :model
end
```

```
# spec/support/shoulda_matchers.rb

Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :rspec
    with.library :rails
  end
end
```
- run rspec 

**COMMIT**

```
config/application.rb 

config.generators do |generate|
		generate.helper false
		generate.assets false
    generate.skip_routes true
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
# spec/requests/api/api_responds_with_collection_of_articles_spec.rb

RSpec.describe 'GET /api/articles' do
  describe 'successfully' do
    before do
      get '/api/articles'
    end

    it 'is expected to return a 200 response status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return all articles' do
      expect(JSON.parse(response.body)['articles'].count).to eq 3
    end

    it 'is expected to return articles titles' do
      expect(JSON.parse(response.body)['articles'].first['title']).to eq 'This is an awesome title'
    end
  end
end
```
- we should get an error that we have no route that matches index

```
routes.rb

Rails.application.routes.draw do
  namespace :api do
    resources :articles
  end
end
```
- That opens up all the routes to the articles endpoint, but we should only have the routes open that we can take care of
```
Rails.application.routes.draw do
  namespace :api do
    resources :articles, only: [:index]
  end
end
```
- show rails routes again

- run Rspec
- add the api folder to our controllers folder. 
- now we need a controller, and that we can generate
```
rails g controller api::articles index
```
- controllers are ALWAYS plural and models are ALWAYS singular, rails is sensitive for naming convention 
- the :: we need to pass to make the controller end up in the correct namespace 

- Run rspec again, ask if anyone knows what a 204 indicates?
- Put a binding.pry in the index method and only run the first test

**COMMIT!**
_____

- We need a model to be able to save articles to our database and then fetch them from there. 
```
rails g model article title:string 
```

- We get a lot of things here. Go over everything that we get. 

```
rails db:migrate
```

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
- Add the validation to the model

- Now back to requests specs, and we can now see that we can ask the model for all articles but it is empty. 
- Lets make use of the factory bot! 

```
# spec/requests/api/api_responds_with_collection_of_articles_spec.rb

RSpec.describe 'GET /api/articles' do
  describe 'successfully' do
  let!(:articles) { 3.times { create(:article) } }
    before do
      get '/api/articles'
    end

    it 'is expected to return a 200 response status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return all articles' do
      expect(JSON.parse(response.body)['articles'].count).to eq 3
    end

    it 'is expected to return articles titles' do
      expect(JSON.parse(response.body)['articles'].first['title']).to eq 'This is an awesome title'
  end
end
```

- Go to the controller and update the index action:
```
  def index
    articles = Article.all
    render json: articles
  end
```
- if we run the test again we can see that we get a 200 but the other tests are not passing. Let's put a binding.pry
- Put it in the test and have a look at the response.body

- Modify the index action:
```
  def index
    articles = Article.all
    render json: {articles: articles}
  end
```
- Use postman to make a request, no articles??
- Go into rails console and create some, make the request again. 

**COMMIT**

```
# spec/requests/api/api_responds_with_one_specific_articles_spec.rb

RSpec.describe 'GET /api/articles/:id' do
  describe 'successfully' do
    let!(:article) { create(:article, title: 'This is the latest news', body: 'And this is some mind blowing content') }

    before do
      get "/api/articles/#{article.id}" #explain this with random id's and get back to that when tests are going green
    end

    it 'is exptected to return a 200 status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return the requested articles title' do
      expect(JSON.parse(response.body)['article']['title']).to eq 'This is the latest news'
    end
  end
end
```
- stop here now and create the response json module and include it in the `rails_helper`

```
module ResponseJSON
  def response_json
    JSON.parse(response.body)
  end
end
```
- Go back to the test and refactor and write a test for the content as well
```
# spec/requests/api/api_responds_with_one_specific_articles_spec.rb

RSpec.describe 'GET /api/articles/:id' do
  describe 'successfully' do
    let!(:article) { create(:article, title: 'This is the latest news', body: 'And this is some mind blowing content') }

    before do
      get "/api/articles/#{article.id}" #explain this with random id's and get back to that when tests are going green
    end

    it 'is exptected to return a 200 status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return the requested articles title' do
      expect(response_json['article']['title']).to eq 'This is the latest news'
    end

    it 'is expected to return the requested articles body' do
      expect(response_json['article']['body']).to eq 'And this is some mind blowing content'
    end
  end
end
```

- And now we can see that we get undefined method for body, because we don't have that in our database. 
- show schema and talk about that file 

```
rails g migration AddBodyToArticle body:text
```

- strings in rails has a limitation, and therefor we can use text instead
- Why don't we just add it to the schema?
- why don't we just go into the previous migration and change that?

- run the migrations, and add the tests about the content to the model spec
- update the factory
- Show the other way of adding validations to the model

- Back to the request spec and now the route is missing, remove the `only` first to show how you can find out how the routes look

- add the show request and put a binding.pry in there
- show the params and talk about that we want to find this article in the db 

```
  def show
    article = Article.find(params['id'])
    render json: {article: article}
  end
```

- run Rspec again 

- and Boom! Everything is green! 


-------

- branch off

```
api_provides_user_to_create_an_article_spec.rb

RSpec.describe 'POST /api/articles' do
  describe 'successfully' do
    before do
      post '/api/articles',
      params: {
        article: {
          title: 'This is a new article',
          body: 'With some brand new content'
        }
      }
    end

    it 'is expected to return a 201 response status' do
      expect(response).to have_http_status 201
    end

    it 'is expected to return a success message' do
      expect(response_json['message']).to eq 'The article was successfully created'
    end
  end
end
```

- run rspec
- here we go again, go to routes and add new

```
articles_controller


  def create
    binding.pry
  end
```
- Try to just pass in `article = Article.create(params['article'])` in pry to show the mass assignment error
```
  def create
    Article.create(article_params)
    render json: { message: 'The article was successfully created' }, status: 201
  end

  private

  def article_params
    params.require(:article).permit(:title, :body)
  end
```
- run rspec
- And we're green! That was fairly simple? 
- But what happens if the title is empty for example?

```
 if article.persisted?
    render json: { message: 'The article was successfully created' }, status: 201
  else
    #we need to do somethign here
    binding.pry
  end
```
- In binding.pry, look at the errors
`article.errors.full_messages.to_sentence`

**COMMIT!**
____

```
api_provides_user_to_edit_an_article_spec.rb

RSpec.describe 'PUT /api/articles' do
  let(:article) { create(:article) }
  describe 'successfully' do
    before do
      put "/api/articles/#{article.id}",
          params: {
            article: {
              title: 'This is the new and cool title'
            }
          }
    end

    it 'is expected to return 201 status' do
      expect(response).to have_http_status 201
    end

    it 'is expected to return success message' do
      expect(response_json['message']).to eq 'The article was successfully updated'
    end

    it 'is expected to update the article' do
      expect(article.title).to eq 'This is the new and cool title'
    end
  end
end
```
- ad update to the routes, why should we keep the only?
- put a binding.pry in the update action and take it one step at the time

```
  def update
    article = Article.find(params['id'])
    article.update(article_params)
    if article.save
      render json: { message: 'The article was successfully updated' }, status: 201
    else
      render json: { message: article.errors.full_messages.to_sentence }, status: 422
    end
  end
```
- Change the last test accordingly: 
```
    it 'is expected to update the article' do
      expect(article.reload.title).to eq 'This is the new and cool title'
    end
```


**Some refactoring if time**

```
 class Api::ArticlesController < ApplicationController
  def index
    articles = Article.all
    render json: { articles: articles }
  end

  def show
    article = Article.find(params['id'])
    render json: { article: article }
  end

  def create
    article = Article.create(article_params)

    if article.persisted?
      success_message('created')
    else
      error_message(article)
    end
  end

  def update
    article = Article.find(params['id'])
    article.update(article_params)
    if article.save
      success_message('updated')
    else
      error_message(article)
    end
  end

  private

  def article_params
    params.require(:article).permit(:title, :body)
  end

  def success_message(action)
    render json: { message: "The article was successfully #{action}" }, status: 201
  end

  def error_message(article)
    render json: { message: article.errors.full_messages.to_sentence }, status: 422
  end
end
```