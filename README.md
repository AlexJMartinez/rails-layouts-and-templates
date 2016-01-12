# Rails Layouts And Templates

## Objectives

After this lesson, you'll be able to...

1. Identify the default application layout.
2. Yield to view templates from a layout.
3. Specify a custom layout in ActionController on a controller level using the `layout` macro and on the action level using the `render :layout => "custom"` option.
4. Use :layout => false to shut off the layout and only render the view

## Life Without Layouts

Imagine that you are tasked to build an online shop app with Rails.

You would probably have a few different pages in this app, for example: 

1. A list of products
2. A detail view that shows more info for a selected product
3. A shopping cart

Across all these pages you would want a consistent look, which is called a layout. This layout perhaps contains something like a logo, navigation links, a search bar, and a footer at the bottom that contains some info about the shop.

Without layouts you would need to copy and paste your logo, navigation, search, and footer code into each action's template that you want in your application.

And when you want to make a change to one of the common components, for example the navigation, you would have to go and make that change in all the template files that you created in your application. This will obviously slow you down a lot.

## Layouts To The Rescue

Luckily you don't need to copy content from one template file to the next, because layouts in Rails are enabled by default, and when you generate a new Rails app, it generates a layout for you. 

To find the generated layout, go and have a look in your Rails app at the following path. When you render a template for an action without specifying a different layout to use, Rails will use the layout found at this location.

#### app/views/layouts/application.html.erb

When you first generate a Rails app, this file will generate something very similar to this, depending on your version of Rails. The application.html.erb file is a very good place to start adding common components, like the navigation, search, and footer from the example above. 

```erb
<!DOCTYPE html>
<html>
<head>
  <title>ACME Store</title>
  <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
  <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
  <%= csrf_meta_tags %>
</head>
<body>

<%= yield %>

</body>
</html>
```

## Yield

Let's say you code up a new layout from scratch, and you end up with something like this:

#### app/views/layouts/application.html.erb

```erb
<!DOCTYPE html>
<html>
<head>
  <title>ACME Store</title>
</head>
<body>

</body>
</html>
```

**Please note:** usually you should include links to assets like style sheets and JavaScript files in your layouts, which was ommitted in the code above to keep it simpler. 

Other than the missing links to common assets, this layout is missing something terribly important. To see what it is, have a look at the following example that uses this layout. 

This is an example of an action that we expect to result in our action's template rendered within the layout defined above.

####/app/controllers/static_controller.rb

```ruby
class StaticController < ActionController::Base
  def about
  end
end
```

There should also be an associated route in the /config/routes.rb file to route a request to **/about** to the about action in the static controller above.

####/config/routes.rb
```ruby
Rails.application.routes.draw do
  get 'about', to: 'static#about'
end
```


Pretty simple README that illustrates how Rails uses layouts in app/views/layouts/application.html.erb as the default layout applied to all views.

Start with why layouts are nice. Notice that every page needs certain things. It would be silly to copy paste every time

Show that the layout is rendered in a simple static example (like an about page) but that the view is not rendered, only the layout is.

explain how we <%= yield %> within a layout to delegate or yield the rest of the rendering to the view specific action template.

Explain that for every request we only ever render one layout and one view, even if multiple html.erb's compose the entire view using something called partials we'll learn about later, but still, it's one layout, one view, and then lots of partials get mixed in.

layouts correspond to controllers or sections of your application (not weird to have an admin layout, a marketing layout and then an application layout).

show the layout controller macro and the conventions between controller layouts (ProductsController will automatically use layouts/products.html.erb if it exists over application.html.erb even though that's rarely useful).

show the render :layout and render :layout => false for view specific layouts.
