# General Workflow FAQ

## Server Questions

#### Question:
> When should I restart my Rails server?

#### Answer:
There are a few specific scenarios in which you should restart your Rails server:

1. After you run `rake db:migrate`
2. After you edit files in your `config` folder
3. After editing model files (such as `place.rb`, `quote.rb`, etc.)
4. After editing controller files

Another way of looking at it is that it is a safe bet to restart your it after editing plain Ruby code (not embedded Ruby) in your application and after running any migrations.

#### Question:
> I am trying to shut down or start my rails server, but I'm seeing this error message:
> `A server is already running. Check /vagrant/src/your-app-name-here/tmp/pids/server.pid.`
> `Exiting`

#### Answer:
If you see this error message, you'll need to use a terminal window inside your web dev environment to navigate into your web application project folder and run the following command:

`kill `cat tmp/pids/server.pid``