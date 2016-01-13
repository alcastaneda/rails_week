##Objectives
-Understand how to make one form for new and edit
-Be able to render form in view
-Know how to perform CRUD actions

##Introduction
We are going to learn how to make a CRUD app in rails today.
Recap: what is CRUD? Create Read Update Destroy
Why should we know this? Core functionality of apps.

routes:
```
resources :books
```
```html
<%= form_for(@book) do |f| %>
    <%= f.label :title %>
    <%= f.text_field :title %><br>
    <%= f.hidden_field :checked_out, value: @checked_out %>

    <%= f.submit %>
<% end %>
```

###Form Helpers
* text_field
* password_field
* text_area
* hidden_field
* radio_button
* check_box
* file_field
* label

##DEMO/Codealong
rails new library_app
rails g model book checked_out:boolean title:string
rails g controller book index show new create edit update destroy

Book
validates :title, presence: true;

touch app/views/books/_form.html.erb

```html
<%= form_for(@book) do |f| %>
    <%= f.label :title %>
    <%= f.text_field :title %><br>
    <%= f.hidden_field :checked_out, value: @checked_out %>

    <%= f.submit %>
<% end %>
```
Let's see if this form works for new
```
def show
        @book = Book.find(params[:id])
  end

  def new
    @book = Book.new
    @checked_out = false
  end

def create
    @book = Book.new(book_params)

    if @book.save
      redirect_to :show
    else
      render :new
    end
end

private 
     def book_params
        params.require(:book).permit(:title, :checked_out)
      end
```
touch app/views/books/new.html.erb

New
```
<h1>New Book</h1>

<%= render 'form' %>
```
touch app/views/books/show.html.erb

Show 
```
<h1><%= @book.title %></h1><br>
<h3>Checked out? <%= @book.checked_out %></h3><br>
```
Now let's make edit
```
  def edit
    @book = Book.find(params[:id])
    @checked_out = @book.checked_out
  end

  def update
    @book = Book.find(params[:id])
    if @book.update(book_params)
      redirect_to :show
    else
      render :edit
    end
  end
```
touch app/views/books/edit.html.erb
```
<h1>Edit Book</h1>

<%= render 'form' %>
```
touch app/views/books/index.html.erb
```
<h1>Books</h1>
<% @books.each do |book| %>
  <h3><%= book.title %></h3>
  <p><%= book.checked_out %></p>
<%= link_to book.title, book_path(book.id) %>
or
  <%= link_to "Show", book_path(book.id) %>
<% end %>
```
##Conclusion

##Independent Practice
