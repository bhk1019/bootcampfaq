# Heroku Troubleshooting FAQ

## General Troubleshooting Tips

If you are running into any issues with Heroku, there are a couple of things that are always useful to try.

Try these common fixes first:

1) Restart the Heroku server by running `heroku restart` in your console.
2) Run any migrations by running `heroku run rake db:migrate`.
3) Reset your entire production database on Heroku by running:
```
heroku restart
heroku pg:reset DATABASE
heroku run rake db: migrate
```

If these steps don't work, then you can view the error logs that are generated by Heroku by running `heroku logs` in your terminal. Search for fixes by googling relevant keywords in the heroku logs.

## Project Specific Tips

### Vagrant Environment Set Up

#### Question:
> When I run `heroku login`, the terminal hangs/takes a really long time to load.

#### Answer:
Try running `heroku login --interactive` instead.

### Splurty

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