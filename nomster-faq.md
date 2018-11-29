# Homepage Slider

## Lesson 46: Styling the Slider

#### Question:
> The carousel on my app's homepage doesn't look right.

#### Answer:
In some cases, the images in your carousel may look stretched, or the CSS may not be applying exactly as expected to your homepage. At this stage, if the rest of your Nomster app is working correctly, you should continue on in the rest of the Nomster lessons lessons.

If you'd like to dive into the details, you can bring any styling issues to your next mentor session.

# User Profile Page

## Lesson 47: User Dashboard Page

#### Question:
> I am getting an error message that says `undefined method 'email' for nil:NilClass` after creating the user profile page and clicking the 'My Profile' link.

#### Answer:
You are likely seeing this message if you created a place, added comments to the place, then deleted the place. When there is no longer a valid place associated with a comment, `comment.place.name` doesn't work anymore because `place` will be nil.

To move past this error, try the following steps (unfortunately, this will mean that any data in your development database is lost - it will not affect anything you have on production on Heroku):
1) Stop your server by hitting `CTRL + C`.
2) Run `rake db:drop:all` - this will delete your database.
3) Then, run `rake db:create:all` to create a new database.
4) Run `rake db:migrate`

From here, you can prevent this issue from occurring in the future by going to your place model file (`app/models/place.rb`) and ensuring that the relationship with comments looks like this: `has_many :comments, dependent: :destroy`

This change to your place model will ensure that whenever you delete a place, its comments will also be deleted and won't show up to cause problems in your app.
