# Adding a Google Map

## Lesson 29: Setting Up the Maps Integration

#### Question:
> My app will only save the latitude and longitude of some addresses and not others. When I investigate in the rails console, I get a "Google API Error: Over Query Limit" message.

#### Answer:
Sometimes, if the address saves as `longitude: nil` and `latitude: nil`, it could be because the Geocoder gem could not successfully locate the coordinates of the given address. First double check that your address is correct.

If the problem persists, this error could be related to your Google API Keys. For some users, it will be necessary to enable billing on your Google API accounts in order to increase your query limit.

Follow these steps to see what your query limit is:
1) Go to console.cloud.google.com.
2) Click on the APIs & Services dashboard on the left side navigation bar.
3) Click on the Geocoding API under the API section.
4) Click on the Quotas tab between Metrics and Credentials.
5) Scroll down to the Requests subsection. Look for "Requests Per Day". If you cannot change this value above "1", then you may currently only be limited to one geocoding request per day and your Google API Account does not have billing enabled.

In order to enable billing on your Google API Account, follow the steps on this page: https://developers.google.com/maps/documentation/geocoding/usage-and-billing . Then, update the Requests Per Day field as described in the steps above to increase your quota. Keep in mind that your account will be billed after 1000 total requests, so set your Requests Per Day to something reasonable to prevent unwanted charges.

# Comments on Places

## Lesson 39: Add an Image

#### Question:
> After uploading an image successfully on my local app and going to my `places/show/html.erb` view, I am seeing an error like this: `ActionView::Template::Error (Can't resolve image into URL: undefined method 'to_model'`

#### Answer:
Go into your `places/show.html.erb` view and change the line that looks like this:

> `<%= image_tag photo.picture %>`

to look like this:

> `<%= image_tag photo.picture.url %>`

Then refresh your app.

#### Question:
> I can successfully upload images via AWS, but they are not showing up in my application. All I see where the images should be is a broken image icon.

#### Answer:
Check your AWS bucket name. If it has a period in it, that can cause problems with uploading. Your browser may stop the image from showing up over HTTPS; if you switch the URL to start with `HTTP`, your image should show up.

To fix this in your application, you can build a new AWS bucket that doesn't contain a period and use that (regenerating the  `application.yml` file, etc.). You followed the steps in the lesson correctly, but AWS has an issue with buckets with period in the name.

After adding a new bucket, you should be able to continue using your existing user and AWS keys. If for some reason that _doesn't_ work, try generating new credentials.

# Sending Emails

## Lesson 42: Adjusting the Mailer

#### Question:
> I am not receiving emails sent to test my mailer setup.

#### Answer:
If you're not seeing any error messages in your terminal, this is likely an account setup issue with your email account. At this stage, it's okay if emails aren't sending from your local environment.

For now in your local environment, use the `:test` environment instead in `config/environments/development.rb`. This will look like changing the line that reads:

> `config.action_mailer.delivery_method = :smtp`

to

> `config.action_mailer.delivery_method = :test`

This way, you can see the HTML content of your email in your server window.

In lesson 44, you'll be able to actually send out emails on your production app once you set up emailing on Heroku with Sendgrid.

## Lesson 43: Send Email on Comment

#### Question:
> I am not receiving emails when I create a comment on my local app.

#### Answer:
If you aren't seeing any error messages when adding comments to places, you should continue on to lesson 44, where you'll set up and send emails on production with Sendgrid.

## Lesson 44: Mailing on Production

#### Question:
> I'm receiving a "Something Went Wrong" error message on Heroku.

#### Answer:
Try these common fixes for Heroku bugs:
1) Restart the Heroku server by running `heroku restart` in your console.
2) Run any migrations by running `heroku run rake db:migrate`.
3) Reset your entire production database on Heroku by running:
```
heroku restart
heroku pg:reset DATABASE
heroku run rake db: migrate
```

# Homepage Slider

## Lesson 46: Styling the Slider

#### Question:
> The carousel on my app's homepage doesn't look right.

#### Answer:
In some cases, the images in your carousel may look stretched, or the CSS may not be applying exactly as expected to your homepage. At this stage, if the rest of your Nomster app is working correctly, you should continue on in the rest of the Nomster lessons.

If you'd like to dive into the details, you can bring any styling issues to your next mentor session.

# User Profile Page

## Lesson 47: User Dashboard Page

#### Question:
> After creating the user profile page and clicking the 'My Profile' link, I am seeing an "undefined method ... for nil:NilClass" error.

#### Answer:
You are likely seeing this message if at some point you created a place, added comments to the place, then deleted the place. When there is no longer a valid place associated with a comment, `comment.place.name` doesn't work anymore because `place` will be nil.

To move past this error, try the following steps (unfortunately, this will mean that any data in your development database is lost - it will not affect anything you have on production on Heroku):
1) Stop your server by hitting `CTRL + C`.
2) Run `rake db:drop:all` - this will delete your database.
3) Then, run `rake db:create:all` to create a new database.
4) Run `rake db:migrate`

From here, you can prevent this issue from occurring in the future by going to your place model file (`app/models/place.rb`) and ensuring that the relationship with comments looks like this: `has_many :comments, dependent: :destroy`

This change to your place model will ensure that whenever you delete a place, its comments will also be deleted and won't show up to cause problems in your app.
