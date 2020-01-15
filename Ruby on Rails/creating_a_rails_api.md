# Creating a Rails API

#### Step 1 - run `rails new app-name --api` in your terminal to create rails api

#### Step 2 - You may want to generate your controllers by now, and to generate, set it under the `api/v1/` directory `rails g controller api/v1/controller-name` 

#### Step 3 - Start creating the controllers and models as needed. A shortcut to this is to generate scaffold or resource and then creating a new directory under controllers as `api/v1` , then move the controllers in the v1 directory, afterwards change the first line of the directory from `class UsersController > ApplicationController` to `class Api::V1::UsersController < ApplicationController` .

#### Step 4 - Setup routing by wrapping your routes with namespace:

``` ruby
 namespace :api do
    namespace :v1 do
      resources :users
    end
  end
```

And if there are two versions of the models then set

``` ruby
 namespace :api do
    namespace :v1 do
      resources :users
    end
    
    namespace :v2 do
      resources :users
    end
  end
```



#### Step 5 - Afterwards seed the database and define the index in the controller with a render of JSON in order to start viewing the data

``` ruby
def index
    @users = User.all
    render json: @users, status: 200
end
```



#### Step 6 - Run the rails server `rails s` and then on your browser, search for `localhost:3000/api/v1/users` to view the data 

#### Step 7 - Setup CORS by uncommenting the `gem 'rack-cors'`  in the gemfile and run bundle install. CORS is the bridge between web and who has access to the API, by limiting how much access does this site have. 

#### Short definition of CORS - Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible

#### Next, go to the `cors.rb` file under `config/initializers/` directory and uncomment this portion of the code 

```ruby
 Rails.application.config.middleware.insert_before 0, Rack::Cors do
   allow do
     origins 'example.com'

     resource '*',
       headers: :any,
       methods: [:get, :post, :put, :patch, :delete, :options, :head]
   end
 end
```

#### And modify the code into this

```ruby
Rails.application.config.middleware.insert_before 0, Rack::Cors do
   allow do
     origins '*' # this wildcard gives access to ANYBODY

     resource '*', # this gives access to ANY RESOURCE
              headers: :any,
              methods: [:get, :post, :put, :patch, :delete, :options, :head]
   end
 end
```

#### Afterwards restart the server (if its active) and test to make sure your code is going through any site

####  









#### Step 8 - 







## Resources / Reference

* #### Mod 3 - Rails as an API

* #### ["How to build a good API using RubyOnRails"](https://codeburst.io/how-to-build-a-good-api-using-rubyonrails-ef7eadfa3078)

* 




