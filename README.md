# rails-module-railsadmin
> Rails module for rails-admin.


## step by step:
+ Add new filed for admin user:
```bash
# gem 'devise'
rails generate devise:install
rails generate devise User

## Or you can add admin field to the migration
# t.boolean :admin
rails g migration AddAdminToUser
```

+ Add auth to posts_contrlller:
```ruby
before_action :authenticate_user!
```

+ check in home_controller:
```ruby
class HomeController < ApplicationController
  def index
    if current_user
      redirect_to posts_path
    end
  end
end
```
+ Add to layout navations:
```ruby
  <% if current_user %>
  <%= link_to 'logout' destroy_user_session_path, method: :delete%>
  <% else %>
  <%= link_to 'login' new_user_session_path %>
  <% end %>
```

+ Install rails_admin
```bash
# gem 'rails_admin'
rails g rails_admin:install
```
+ set authorization:
```ruby
  config.authorize_with do
    redirect_to main_app.root_path unless warden.user.admin == true
  end
```

+ result:
```conf
1290657123@qq.com/admin true  ===> Can edit post/user 
other@qq.com /admin false     ===> Can not ....
```


## resources:
+ https://github.com/sferik/rails_admin