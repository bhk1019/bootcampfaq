# Getting Started

## Lesson 1: Set Up a Development Environment and Start a New Project

#### Question:
> When I run `heroku login`, the terminal hangs/takes a really long time to load.

#### Answer:
Try running `heroku login --interactive` instead.

#### Question:
> I'm using the Vagrant install process. When I run `curl https://raw.githubusercontent.com/university-bootcamp/coding-environment/cloud-ide-instructions/github_auth.rb > ~/.bootcamp-github.rb && ruby ~/.bootcamp-github.rb` I get a 404 error message.

#### Answer:
Try the following steps:
1) Run the command `gem install github_api` in your terminal.
2) Once the install finishes, run `touch .bootcamp-github.rb`.
3) That command should have made an empty file called `.bootcamp-github.rb`. Find this file and open it in your text editor. It should be a hidden file inside of the `coding-environment` folder. If you press `Command + Shift + .` on a Mac you can view hidden files in the Finder.
4) Then, copy and paste the following into the empty `.bootcamp-github.rb` file:
```
require 'github_api'
require 'io/console'

# Bypass annoying deprecation warning between the
# github_api gem and the faraday gem
Faraday::Builder = Faraday::RackBuilder

print "Github Username: "
user_name = gets.strip
print "Github Password (nothing will be displayed):"
password  = STDIN.noecho(&:gets).strip
github = Github.new(:login => user_name, :password => password)
github.users.keys.create("title" => "FirehoseVagrant", 
    "key"=> File.open("/home/vagrant/.ssh/id_rsa.pub").read)
puts "\nok!"
```
5) Once you do that, save the `.bootcamp-github.rb` file. In your terminal, run `ruby .bootcamp-github.rb`.

#### Question:
> I have the same problem as the question above, but I'm using Codenvy.

#### Answer:
Try the following steps:
1) Run `cat ~/.ssh/id_rsa.pub`. If there is no output, make sure you have already generated a public SSH key by following these steps: https://github.com/university-bootcamp/coding-environment/blob/master/account-setup.md#step-1-generate-ssh-key
2) Copy the output of the last command.
3) Go to `github.com` and sign in. In the upper right hand corner, click your profile photo, then select Settings.
4) Click SSH and GPG Keys.
5) Click New SSH Key.
6) Name the key (something like Codenvy should be fine), then paste the output from Step 1 into the Key field, and then click Add SSH Key.

#### Question:
> When trying to start the server on Codenvy, I'm receiving an error instead of the "Yay! You're on Rails!" page. The error says something like: `could not connect to server: Connection refused. Is the server running on host "localhost" and accepting TCP/IP connections on port 5432?`.

#### Answer:
Try restarting your postgres database by changing to the root directory and running: `/etc/init.d/postgresql restart`.

## Lesson 11: Add a Footer

#### Question:
> None, or only some, of the CSS styles are applying to my website.

#### Answer:
Double check that you have followed the bootstrap install process according to the guide in Lesson 7. The bootstrap install documentation on Github differs slightly from the guide in Lesson 7.

## Lesson 15: Building the About Page

#### Question:
> How do I get rid of old quotes that I don't want to show up on my app?

#### Answer:
To get rid of data in your local machine, you do the following:
1) Open the rails console by running `rails console` in the terminal.
2) Find and destroy the bad quote by using `Quote.find().destroy`. (Note: this command is case sensitive!) You'll need to identify the id number of your bad quote and enter it as a parameter to `find`. For example, if the id of the bad quote is `5`, then you would input `Quote.find(5).destroy`. To view all quotes, you can run `Quote.all` and you should be able to see the id of the quote that you want to get rid of. If there are too many quotes to view in the output after using `Quote.all`, then run `Quote.all.as_json` to view all quotes in a different format (the JSON format).

To get rid of data on your Heroku server, you can do the same steps as above, but in the Heroku rails console. Access this by running `heroku run rails console` in step 1 above instead of `rails console`. Then proceed with step 2.

## Lesson 18: Deploy Your Web App

#### Question:
> When I run `git push heroku master` there are no errors, but when I check my live website, it doesn't match what I see on my localhost. What should I do?

#### Answer:
Double check that you have pushed your most recent changes to git before you ran `git push heroku master`. You can check the status of your updated files by running `git status` in the terminal. Heroku will pull changes from git, and not your local machine, so you need to run through the git workflow first before pushing to heroku.

If your site looks otherwise functional, but with different quotes than what is on your localhost, this is perfectly normal. There are two databases, the `development` databse and the `production` database. The quotes that are saved on your `production` database (located on your local machine) will be different from the quotes that are saved on your `production` database (stored on Heroku's servers).

#### Question:
> When I run `git push heroku master` there is an error message. I can't complete the push to Heroku.

#### Answer:
Try the following steps first:
1) Make sure that you have run `heroku run rake db:migrate` and `heroku restart` to run any migrations on your database.
2) Make sure that you have at least one quote on your production database. To add one in, you can use `heroku run rails console` to enter the Heroku rails console. Then run `Quote.create(saying: "test quote", author: "test author")`.
