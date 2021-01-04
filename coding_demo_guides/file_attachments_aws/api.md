```ruby
RSpec.describe 'POST /article', type: :request do
  let(:journalist) { create(:user, role: 'journalist') }
  let(:journalist_credentials) { journalist.create_new_auth_token }
  let(:journalist_headers) do
    { HTTP_ACCEPT: 'application/json' }.merge!(journalist_credentials)
  end

  describe 'successfully' do
    before do
      post '/api/articles',
           params: {
             article: {
               title: 'No more room in space',
               snippet: 'Its all gone, sorry',
               content: 'Govenor says this aint good',
               category: 'tech',
             }
           },
           headers: journalist_headers
    end

    it 'returns 200 status' do
      expect(response.status).to eq 200
    end

    it 'displays correct title' do
      expect(
        response.request.params['article']['title']
      ).to eq 'No more room in space'
    end

    it 'displays correct snippet' do
      expect(
        response.request.params['article']['snippet']
      ).to eq 'Its all gone, sorry'
    end

    it 'displays correct content' do
      expect(
        response.request.params['article']['content']
      ).to eq 'Govenor says this aint good'
    end

    it 'displays correct category' do
      expect(response.request.params['article']['category']).to eq 'tech'
    end

    it 'article has an image attached to it' do
      article = Article.where(title: response.request.params['article']['title'])
      expect(article.first.image.attached?).to eq true
    end
  end
end 
```
- active storage is one of the frameworks withing rails, facilitates uploading files to different cloud services as AWS, microsoft Azure, google cloud and so on.

```
$ rails active_storage:install:migrations
```
- the attachment is the link between the file and the active storage object (the resource created)
- the blob is the actual file, so it is associated with the attachment 

- go to the model and add 
```ruby
has_one_attached :image
```

```ruby
  let(:image) do
    {
      type: 'application/jpg',
      encoder: 'name=new_image.jpg:base64',
      data: 'GHJKFNKSJHFUDHFdnfkdjfjkshuhFNLNKLFDFJLkjksldjflkgdmsk248273rendlksfn',
      extension: 'jpg'
    }
  end
  # and add it to the params
```
```ruby
# articles controller
def create 
  #...
  if article.persisted & attach_image(article)
  #...
end
private 

def attach_image(article)
  params_image = params[:article][:image]
  if params_image.present?
    DecodeService.attach_image(params_image, article.image)
  end
end
```
- create a new folder in the app folder called `services` and a new file called decode_service.rb

```ruby
module DecodeService 
  def self.attach_image(file, target)
   image = Rails.env.test ? file : split_base64(file)
   decoded_data = Base64.decode64(image[:data])
    io = StringIO.new
    io.puts(decoded_data)
    io.rewind

    target.attach(io: io, filename: "#{image[:encoder]}.#{image[:extension]}")
  end

private_methods

  def self.split_base6(string)
    if string =~ /^data:(.*?);(.*?),(.*)$/
      uri = {}
      uri[:type] = Regexp.last_match(1)
      uri[:encoder] = Regexp.last_match(2)
      uri[:data] = Regexp.last_match(3)
      uri[:extension] = Regexp.last_match(1).split('/')[1]
      uri
    end
  end
end

```
- now we have the image, but we need to store it in the cloud instead of in our own database

- we need to add a gem for using AWS

```ruby
gem 'aws-sdk-s3'
```
- bundle! 

- go to the storage.yml
- comment back in the amazon option
```yaml
region: eu-north-1
bucket: the-bucket-you-have-got
```

- add the credentials for aws to the credentials file

- go to environments and development and production and change the active storage to :amazon instead of local. 


### To send images with the article
```ruby
#articles model
  def image_path
    Rails.env.test? ? ActiveStorage::Blob.service.path_for(image.key) : image.service_url(expires_in: 1.hour, disposition: 'inline')
  end
```
```ruby
#articles serializer
    return nil unless object.image.attached?

    object.image_path
```
