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