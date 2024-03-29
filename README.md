#D3 Rails "Hello World" App

This is a basic app that employs the simplest approach to adding a D3 chart. I did not want to create any models or modify any controllers. Just create a static view that renders a chart.

###D3.js
D3.js is a JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG, and CSS. (From [d3js.org](http://d3js.org/) website)

---
**Here are the steps:**

* Create static page controller
```ruby
    rails generate controller StaticPages home
```

* Add javascripts to `config/initializers/assets.rb`:
```ruby
    Rails.application.config.assets.precompile += %w( d3.js )
    Rails.application.config.assets.precompile += %w( d3example.js )
```

* Add D3 scripts to `vendors/javascripts` (i.e., `d3.js` from http://d3js.org/)

* Add custom javascripts to `app/assets/javascripts`

* Add stylesheet to `app/assets/stylesheets`

* Update `app/views/application.html/erb` to include

    `<%= yield(:head) %>` and `<%= yield(:body) %>`

```html
    <!DOCTYPE html>
    <html>
    <head>
      <title>D3app2</title>
      <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
      <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
      <%= csrf_meta_tags %>
      <%= yield(:head) %>
    </head>
    <body>
      <%= yield %>
      <%= yield(:body) %>
    </body>
    </html>
```

* Add `content_for` tags to `home.html.erb` to call the page specific javascripts:

```ruby
    <% content_for :head do %>
      <%= javascript_include_tag 'd3' %>
    <% end %>

    <h1>D3 Hello World</h1>

    <% content_for :body do %>
      <%= javascript_include_tag 'chart' %>
    <% end %>
```

* Put data in the `public` folder

**That's it!**

---
###Credits

- http://d3js.org/
- Chart taken from: http://bl.ocks.org/mbostock/4062045
