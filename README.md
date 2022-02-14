# Demo Generate Image (API)

Generate image from 3rd party API provider [shibe.online](https://shibe.online)

## Setup

```bash
rails db:drop db:create db:migrate
```

## Running server

```bash
rails s
```

## Endpoint

```bash
GET http://localhost:3000/dogs
```

Output,

```json
[
    "https://cdn.shibe.online/shibes/44b7e7feebe11995801d9def270de09d6c38423f.jpg",
    "https://cdn.shibe.online/shibes/9a7bc30ed526ee0acb3201daa3bf61519f6f1710.jpg",
    "https://cdn.shibe.online/shibes/97b7092851e10d5903d7a7e169ccb4e081ba5be8.jpg",
    "https://cdn.shibe.online/shibes/bae2f71b52330a8397ce6857161633294d2f2b5c.jpg",
    "https://cdn.shibe.online/shibes/f3d8687c19ac58e58ba420d58d2f2eb32c92b426.jpg",
    "https://cdn.shibe.online/shibes/175d2306f49ea49f924d386df37beba2c599c3ca.jpg",
    "https://cdn.shibe.online/shibes/f5c26fb900bcdb2de1b015f46ef9f63e563ded89.jpg",
    "https://cdn.shibe.online/shibes/14bf2ca9ed173a3e6c5962f0b04294b68aa162a7.jpg",
    "https://cdn.shibe.online/shibes/f2bd9726224c895d95b6ea391c4373fcefa564d7.jpg",
    "https://cdn.shibe.online/shibes/c418a425ff166639d50cf7fd782c413f9372bdd6.jpg"
]
```

## Summary

```ruby
# app/controllers/pets_controller.rb
class PetsController < ApplicationController

  require 'rest-client'

  def get_dogs
    url = 'https://shibe.online/api/shibes?count=10'
    response = RestClient.get(url)
    render json: response
  end
end

# config/routes.rb
Rails.application.routes.draw do
  resources :pets
  get '/dogs', to: 'pets#get_dogs'
end
```

## Generate history

```bash
rails g resource Pet image
```

## Refference

1. [Rails Backend: How to Fetch Data From a Third-Party API via RestClient](https://jefferson-cuartas.medium.com/rails-backend-how-to-fetch-data-from-a-third-party-api-via-restclient-c6968e70d6f5)
