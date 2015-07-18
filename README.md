## Overview
- Sign up / Sign in & Out
- Submit a link with a Title & URL
- Vote up or down on a link
- Comment on links submissions

![alt text](http://i.imgur.com/WA2pnhx.png "Home")

## Some notes on this project
### div_for

Structure: `div_for(record, *args, &block)`
Purposes:
- Produces a wrapper DIV element with id and class parameters that relate to the specified Active Record object. In particular, id's name is name of object plus its id, class's name is name of object.

Ex: `div_for(comment) do %>` -> `<div class="comment" id="comment_4">`
- Integrate with render method in View. By pass a collection of Active record to render, which will then get iterated over and yield each record as an argument for the block.

Ex: `<%= render :partial => @link.comments %>` -> `<div class="comment" id="comment_4">...<div class="comment" id="comment_5">`

### Creating a new user, new link or new comment

- Create a user `@user = User.new(user_params)`
- Create a link: many-to-one relationship: for example, the rela of link and user
`@link = current_user.links.build(link_params)`
- Create a comment: `@comment = @link.comments.build(comment_params)`

### Routing
- Nested route:

`resources :links do
  resources :comments
end`

One of routes like that:

`new_link_comment GET /links/:link_id/comments/new(.:format) comments#new`

`edit_link_comment GET    /links/:link_id/comments/:id/edit(.:format) comments#edit`

- One `resources` creates 8 routes
- Use: `rake routes` to show full of routes on app
