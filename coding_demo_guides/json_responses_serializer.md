- use this repo: https://github.com/emtalen/json_response_demo
(Or similar set up where articles belongs to user as author, has many comments and comments belongs to user and article and user has many articles and comments)
- Talk a bit about json responses - use cases for when we want to be in control of them and also that we want to keep the controllers deal with the right responsibility. 

- show background of the application we start with. 

    - article 
      - show and index action
      - Article belongs to user as author, and has many comments
    - comments
      - create action
      - belongs to user and article
    - user 
      - has many articles as author
      - has many comments 
    - show seed file

- show the code in the controller, make a get request to both index and show action
- no keyword of the response
- we don't get the comments and only the author id, we can't really do much with that
- we don't have an authors controller

- show jbuilder on github
- normally in the scaffold 
- like a view layer for api's, so you have to create a file in your views folder

- add jbuilder gem

```
$ mkdir app/views/api/
```
```
$ mkdir app/views/api/articles
```
```
$ touch app/views/api/articles/index.json.jbuilder
```
```
#views/api/articles/index.json.jbuilder 

json.set! 'articles' do
  json.array! @articles do |article|
    json.(article, :id :title, :lead)
    json.created article.created_at.strftime('%F')
    json.author article.author.email
  end
end
```
```
  def index
    @articles = Article.all
    # render json: articles
  end
```
- make the index call to see the response
```
$ touch app/views/api/articles/show.json.jbuilder
```
```
#views/api/articles/show.json.jbuilder 

json.set! 'article' do
  json.(@article, :id, :title, :lead, :body)
    json.created @article.created_at.strftime('%F')
    json.author @article.author.email
end
```
```
 def show
    @article = Article.find(params[:id])
    # render json: article
  end
```
- If anyone asks about nesting things
```
json.set! 'articles' do
  json.array! @articles do |article|
    json.(article, :title, :body)
    json.created article.created_at.strftime('%F')
    json.author do
      json.email article.author.email
      json.name article.author.name
    end
  end
end
```

- change the keyword of the whole response, to show how that works. 
- change a keyword of an attribute to show how that works
- You need to use instance variables 

- Cool, this all looks nice and neat, but lets have a look at active model serilizer 

- add active model serializer gem 
```
gem 'active_model_serializers'
```

```
# config/initializers/ams.rb

ActiveModelSerializers.config.adapter = :json
```
```
$ rails g serializer ArticlesIndex
```
```
class ArticlesIndexSerializer < ActiveModel::Serializer
  attributes :id, :title, :body, :author

  def author
    object.author.email
  end
end
```
```
 def index
    articles = Article.all
    render json: articles, each_serializer: ArticlesIndexSerializer
  end
```
- so what is the difference? It is a matter of opinion
- this is a bit more ruby-isch and we don't have to write json. 100 times and so on. It is more straight forward and more readable

```
class ArticlesIndexSerializer < ActiveModel::Serializer
  attributes :id, :title, :body, #:author
  belongs_to :author

  def author
    {
      email: object.author.email,
      name: object.author.name
    }
  end
end
```
- so we can easily format the response how we want
- we can also add the comments that belongs to the specific article
- So we can have a look at that in the show action
```
$ rails g serializer ArticleShow
```
```
    attributes :id, :title, :body, :author
    has_many :comments

  def author
    {
      email: object.author.email,
      name: object.author.name
    }
  end
```
```
  def show
    article = Article.find(params[:id])
    render json: article, serializer: ArticleShowSerializer
  end
```
- then we get the comments as they are, so here we can add a serializer for the comments 

```
has_many :comments, serializer: CommentsSerializer
```
```
$ rails g serializer comments
```
```
class CommentsSerializer < ActiveModel::Serializer
  attributes :id, :body, :user

  def user
    object.user.name
  end
end
```
- show them to group the serializers into folders
- you can name them what ever you want and should give them a descriptive name