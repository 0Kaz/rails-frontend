
# Watchlist Cheatsheet


:: [select2](https://kitt.lewagon.com/knowledge/tutorials/select2)
:: [sweetalert](https://kitt.lewagon.com/knowledge/tutorials/sweetalert)

***Content***
 - [Reminder](#reminder)
      - [generate controllers and models](#generate-controllers-and-models)
      - [destroy controllers and models](#destroy-controllers-and-models)
      - [Resources](#resources)
      - [collection](#collection)   
      - [member](#member)
      - [Nested Resources](#nested-resources)
      - [Filter Resources](#filter-resources)
 - [SCSS](#SCSS)
 - [SETTING UP YOUR FRONT-END ENVIRONMENT](#SETTING-UP-YOUR-FRONT-END-ENVIRONMENT)
      - [Use Le Wagon's Stylesheets](#Use-Le-Wagon's-Stylesheets)
 - [Associations and validations](#Associations-and-Validations)
      - [What if we have 3 models ?](#What-if-we-have-3-models-?)
      - [Validate presence](#Validate-presence-)
      - [Validate uniqueness](#Validate-uniqueness)
      - [Validate inclusion](#Validate-inclusion)
      - [Validate dependency ](#Validate-dependency-)
      - [Validate integer only](#Validate-integer-only)
      - [Validated minimum lenth in character](#Validate-minimun-length-in-character)      
      - [Validate integer greater or lesser](#Validate-integer-greater-or-lesser)      
      - [Validate more attributes in a scope for uniqueness](#Validate-more-attributes-in-a-scope-for-uniqueness)      


:warning: Make sure that ```yarn``` is installed in all your computers 


# Reminder

### generate controllers and models 

**In your terminal**
```console
    rails g controller controller_name 
    rails g model model_name
```

### destroy controllers and models 

**In your terminal**
```console
    rails d controller controller_name 
    rails d model model_name
```


### Resources 

```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model
end
```


### collection

```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model do
    collection do 
        get :new_action # URI Pattern will be /name_of_your_model/new_action
    end
  end
end
```

### member

```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model do
    member do 
        get :new_action # URI Pattern will be /name_of_your_model/your_model_id/new_action
    end
  end
end
```


### Nested Resources 


```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model do 
    resources :name_of_the_model_nested_model
  end
end
```


### Filter resources

**only**
```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model, only: [:action]
end
```

**except**
```ruby 
Rails.application.routes.draw do
  get 'pages/home'
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  resources :name_of_your_model, except: [:action]
end
```

## SCSS

SCSS is a powerful way to write css, the main idea is to write **less and simpler css to do more styling**


**Example on ```application.scss```**

```scss
 $gray: #F4F3; // <= Similar to inside a variable a value , the variable is '$gray'
 $spacer: 39px;

 body {
     background-color: $gray;
 }

 .btn { 
     padding: $spacer ;

     &:hover{
         color: white;
         background-color: black;
     }

 }
```

You've been doing this for a while now, today you understand the reason why we prefer using ```scss``` instead.

Rename your file ```app/assets/stylesheets/application.css``` to ```app/assets/stylesheets/application.scss```



# SETTING UP YOUR FRONT-END ENVIRONMENT

## BOOTSTRAP

Today's challenges is all about using Advanced Routing and CRUD, it's best to work on a better front-end, we can for now use **Bootstrap** until tomorrow course that will be about front-end in Rails. 

```console
yarn add bootstrap 
```

```console
rm app/assets/stylesheets/application.css
touch app/assets/stylesheets/application.scss

```

Add this on your ```application.html.erb``` layout to make sure bootstrap is more responsive

```html
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
```

## simple_form 

Let's re-use simple_form on these challenges as well 

Add this on your Gemfile :
```ruby 
gem 'simple_form'
```

Don't forget to bundle install & generate simple_form :wink:

```code 
bundle install
rails generate simple_form:install --bootstrap
```

## add these gems as well on your ```Gemfile```

```ruby
gem 'autoprefixer-rails', '10.2.5'
gem 'font-awesome-sass', '~> 5.6.1'
```


## Use Le Wagon's Stylesheets


**On your terminal in your rails project**
```console
rm -rf app/assets/stylesheets
curl -L https://github.com/lewagon/rails-stylesheets/archive/master.zip > stylesheets.zip
unzip stylesheets.zip -d app/assets && rm -f stylesheets.zip && rm -f app/assets/rails-stylesheets-master/README.md
mv app/assets/rails-stylesheets-master app/assets/stylesheets
```


## Associations and Validations 

### What if we have 3 models ? 

Remember the consultation examples we did on our Active Record - Association & Validation courses ?

We had access to a doctor patient *through* consultations 

![cloud](https://res.cloudinary.com/kzkjr/image/upload/v1635425946/blogging/Capture_d_e%CC%81cran_2021-10-28_a%CC%80_13.56.30.png)

```ruby
class Patient < ActiveRecord::Base
  has_many :consultations
end
```

```ruby
class Consultation < ActiveRecord::Base
  belongs_to :patient
  belongs_to :doctor
end
```

```ruby
class Doctor < ActiveRecord::Base
  has_many :consultations

  has_many :patients, through: :consultations
end
```

### Validate presence 

```ruby 
    validates :column, presence: true 
```

### Validate uniqueness

```ruby 
    validates :column, uniqueness: true 
```

### Validate inclusion

```ruby 
    validates :column, inclusion: {in: your_fixed_list_as_an_array }
```

### Validate dependency 

```ruby 
    validates :column, dependent: :destroy
```

### Validate integer only 

```ruby
  validates :column, numericality: { only_integer: boolean_value }
```

### Validate minimun length in character

```ruby
  validates :column, length: { minimum: 6 }

```

## Validate integer greater or lesser 

```ruby
  validates :column, numericality: { greater_than_or_equal_to: 0, less_than_or_equal_to: 10}
```

### Validate more attributes in a scope for uniqueness

```ruby
 validates :column, uniqueness: { scope: :second_column,
    message: "you can leave a message here" }
```



