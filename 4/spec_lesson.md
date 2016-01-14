##Model Testing

rails new rails_rspec
rails g model article title body

validates :title, presence: true
validates :body, presence: true

put in gemfile:
  gem 'rspec-rails'
  gem 'shoulda-matchers'

bin/rake db:migrate RAILS_ENV=test

shows all generators:

rails g

want rspec generators

rails g rspec:install

rails g rspec:model article

rspec spec/models/article_spec.rb

```
let(:blog){Article.new(title:"everthing is awesome", body: "everything is cool when you're part of a team.")}

describe 'validations' do
    it 'saves the article when the fields are not blank' do
        expect{blog.save}.to change{Article.count}.by(1)
    end
end
```

```
let(:blog_no_title){Article.new(body:'hello')}
let(:blog_no_body){Article.new(title:"hello")}

context 'validations' do
    it 'when title is empty' do
        blog_no_title.save
        expect(blog_no_title.errors[:title]).to include("can't be blank")
    end

    it 'when body is empty' do
        blog_no_body.save
        expect(blog_no_body.errors[:body]).to include("can't be blank")
    end
end
```
