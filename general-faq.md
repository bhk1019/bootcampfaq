# General FAQ

## Most Common Issues with an Easy Fix That You Should Know

### Coding-Environment Set Up Process
> Currently, in the official copy of the bootcamp, students are advised to use Codenvy for the Intro Course and Vagrant for the rest of the courses. You should know that Codenvy is not reliable. In particular, TAs have observed these major issues with Codenvy:

1. When creating an `application.yml` file to store API Keys in environment variables, sometimes Codenvy will not persist the file from session to session. The first time students have to do this is in Nomster Lesson 29.
2. One student in the past has had her entire database not persist data from session to session. I believe this happened in Flixter.

> Both of these issues, while not totally impossible to work around, cause students to lose a lot of time, and can lead to them getting frustrated. For this reason, I recommend that you advise students to always try to set up Vagrant, unless they are in the Intro Course.

> One question that has come up is "Can I use a different Cloud IDE than Codenvy". The answer is yes, only in the Intro Course, as long as it can run Ruby scripts. However, I haven't personally QA'd any other options. The Curriculum Team is currently working on a reliable Cloud IDE backup option for students.

#### Issue:
> The student's Vagrant environment times out when they run `vagrant up` for the first time.

#### Solution:
First, check if the student is on Windows. If they are, then ask them to check the Task Manager (`ctrl+shift+esc`) and send you a screenshot of the "Performance" tab. If the "Virtualization" field is `Disabled`, then they will need to enable Virtualization in the BIOS for their machine before Vagrant will boot up. This process is very straightforward and many students have been able to do this on their own. If you direct a student to google "Virtualization enabling for `MAKE OF MY COMPUTER HERE`" then they should be able to figure it out. However, you should offer to help a student who feels uncomfortable going into the BIOS on their own. To do this, ask the student to prepare by:
1. Having Zoom or some other way to communicate with you on their phone (they can't video call you while in the BIOS)
2. Sending you the system information for their Windows machine so that you can research how to enable virtualization for their particular machine.

#### Issue:
> The student is trying to link SSH Keys to their Github account and receiving a 404 error after running this command: `curl https://raw.githubusercontent.com/university-bootcamp/coding-environment/cloud-ide-instructions/github_auth.rb > ~/.bootcamp-github.rb && ruby ~/.bootcamp-github.rb
`

#### Solution:
There's a known fix to this. Tell the student to use this command instead: `curl https://raw.githubusercontent.com/university-bootcamp/coding-environment/master/github_auth.rb > ~/.bootcamp-github.rb && ruby ~/.bootcamp-github.rb`

The Curriculum Team is currently working on correcting the erroneous command in the coding environment setup instructions so hopefully this issue won't come up anymore.

#### Issue:
> The student is running into Github issues in general. Such as: "my `git push` won't recognize the repository", "there is no remote repository recognized", etc.

#### Solution:
The Github documentation on how to link one's machine with SSH to Github is pretty good and straightforward. Many students have been successful troubleshooting these kinds of issues on their own, but you should familiarize yourself with the process as well. Read through all of the documentation here: https://help.github.com/en/articles/connecting-to-github-with-ssh

### The `undefined method current_sign_in_at` Error.

#### Issue:
> The student is receiving a Rails error that says `undefined method current_sign_in_at` seemingly out of nowhere, even though their app was working fine before.

#### Solution:
This is a common issue that arises any time a student is using the *Devise* gem. The first time students have to do this is in Nomster 16. The `current_sign_in_at` method is provided by Devise as part of the Trackable module. In order for a student to use this method in their app, they need to:

1. include the `:trackable` module in the `User.rb` model file
2. migrate all of the columns associated with the `:trackable` module. This means they have to uncomment all of the lines under `#Trackable` in the initial migration file that is generated when the student runs `rails generate devise User`, which is probably called `TIMESTAMP_devise_create_users.rb`.

It's likely the student hasn't done one or either of these steps and moved on through the lessons. If this is the case, then they may have difficulty creating new migrations to fix the User table.

The most straightforward solution is to edit the `devise_create_users.rb` migration file to have *uncommented* all four Trackable methods, then to save and reset the database. This means they will have to run `rake db:drop`, `rake db:create`, and `rake db:migrate`. Note that this will delete all sample/test data in the student's developement database, so be sure to communicate this to the student.

### The `precompiling assets failed` Error when pushing to Heroku.

#### Issue:
> The student's app works fine locally, but receives this error when pushing to Heroku.

#### Solution:
Go through this checklist with the student:
1. Make sure all files in `app/assets/stylesheets` has the extension `.scss` and not `.css`, especially any stylesheets called `fonts`.
2. Make sure all fonts are located in the `app/assets/fonts` folder and not nested in any folders inside of that. For example, make sure there isn't an `app/assets/fonts/fonts` folder.

### Tips on Helping Students Through Nomster 39
> Nomster 39, which is the photo upload feature, will provide the biggest challenge for students in this course and the largest quantity of questions by far comes through this lesson. This is due to the fact that this lesson requires students to implement a pretty complex feature from start to finish with much less guidance than they are used to:
1. They need to create a new model.
2. This model needs to be associated with other models properly.
3. This model needs to have its related database migrations set up properly.
4. They need to install and configure an unfamiliar new gem by reading its documentation.
5. They need to make changes to a view to display data associated with this model.
6. They need to link their app with an unfamiliar new API.

> Due to the self-guided nature of this lesson, I recommend that you take as much of a "hands off" approach as possible, encourage students to ask high quality questions, encourage students to ask themselves where their own gaps in understanding are, and to provide conceptual explanations when necessary. I also recommnend getting on a video call with the student because many errors in this Lesson arise from several conflicting problems and therefore may be difficult to chase down asynchronously. Also, students really respond well to the feeling of having a person walk through the lesson with them.

You can of this lesson as having three major checkpoints:
1. The models, controllers, and views need to be set up correctly.
2. An uploaded photo needs to show up on the local machine.
3. An uploaded photo needs to show up on the production site.

> Go through the following checklists of common mistakes with the student or on your own while looking through the student's repo.

#### The models, controllers, and views need to be set up correctly:

1. A model called `photo.rb` (not `picture.rb`) exists.
2. `has_many :photos` is in `user.rb`
3. `belongs_to :user` is in `photo.rb`
4. `user_id` and `picture` are columns under the `Photos` table (check `schema.rb`)
5. A controller called `photos_controller.rb` exists.
6. `photo_params` in `photos_controller.rb` requires `:photo` and permits `:picture`.
7. The `@photo` variable is initialized with `Photo.new` inside of the `places#show` action.

#### An uploaded photo needs to show up on the local machine:

1. The `places/show.html.erb` view needs to iterate through all photos, using something like `@place.photos.each do |photo| { image_tag photo.picture.url } end`. You may have to play around with removing the `.url`.
2. Carrierwave needs to be installed.
3. The `carrierwave.rb` file needs to exist inside of `config/initializers`.
4. `mount_uploader :picture, PictureUploader` is in `photo.rb`
5. The `picture_uploader.rb` file needs to exist in the `app/assets/initializers` folder.

> If all this has been checked off and the student is receiving an error message: `name error: uninitialized constant Photo::PictureUploader`, then try this fix:

Add the line `require 'carrierwave/orm/activerecord'` to `environment.rb`.

#### An uploaded photo needs to show up on the production site.

> One common issue is the error: `EXCON::ERROR::FORBIDDEN in PhotosController#Create, Expected(200)<=>Actual(403 Forbidden)` when trying to upload photos using Amazon S3. The fix is:

Enable Public Access through the Amazon S3 IAM Dashboard for the bucket you are using for this app.
