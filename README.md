# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
# FlashMessageApp
 1: Add Flash partial on Layout and render flash on Application header
 ###
<div data-controller="flash">
    <% flash.each do |key, value| %>
        <%= content_tag :div, value, id: key %>
    <% end %>
</div>

 ##
 2: Add flash controller in javascript 
 Note: data-controller="flash" et le partial doivent avoir le meme nom

 3: controller:
  create methode:
    if @post.save
        #Flash Message
        flash.now[:notice] = "#{@post.title} added at #{Time.zone.now}" 
        #Turbo_Stream 
        format.turbo_stream do 
          render turbo_stream: [
            #reinitialiser new form
            turbo_stream.update( Post.new, ""),
            #list post in Index
            turbo_stream.prepend("posts", @post),
            #Flash with turbo_stream
            turbo_stream.prepend("flash", partial: "layouts/flash")
            ]
        end
    end