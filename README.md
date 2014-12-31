Hubot
================================================================================

[![Deploy](https://www.herokucdn.com/deploy/button.png)][deploy]

This is a version of my private chatterbot, [hubot][] on [Slack][]. He's pretty cool.

This version is designed to be deployed on [Heroku][].

[hubot]: https://hubot.github.io
[heroku]: http://www.heroku.com
[deploy]: https://heroku.com/deploy
[slack]: https://slack.com


Table of Contents
--------------------------------------------------------------------------------

- [Development](#development)
    - [Requirements](#requirements)
    - [Getting Started](#getting-started)
    - [Testing Hubot Locally](#testing-hubot-locally)
    - [Initial setup to Heroku](#initial-setup-to-heroku)
    - [Slack configuration](#slack-configuration)
- [Scripting](#scripting)
    - [DIY](#diy)
    - [hubot-scripts](#hubot-scripts)
    - [external-scripts](#external-scripts)
- [Operation](#operation)
    - [Deployment](#deployment)
    - [Restart the bot, watch logs](#restart-the-bot-watch-logs)
    - [Checking environment variables](#checking-environment-variables)


Development
--------------------------------------------------------------------------------

### Requirements

- Node.js
- npm
- Redis
- [app.json](https://github.com/app-json/app.json) (Recommended)


### Getting Started

Clone this repository:

```sh
$ git clone git@github.com:Tomohiro/hubot.git
```

Install dependencies:

```sh
$ npm i
```


### Testing Hubot Locally

You can test your hubot by running the following:

```sh
$ redis &
$ bin/hubot
```

Then you can interact with hubot by typing `hubot help`:

```
Hubot> hubot help

Hubot> animate me <query> - The same thing as `image me`, except adds a few
convert me <expression> to <units> - Convert expression to given units.
help - Displays all of the help commands that Hubot knows about.
...
```

Do you want to quit? Just type `hubot die`:

```
Hubot> hubot die
Hubot> Goodbye, cruel world.
```

### Initial setup to Heroku

Create a Heroku app:

```sh
$ heroku create {YOUR_HUBOT_APP_NAME}
```

Add Redis addon:

```sh
$ heroku addons:add rediscloud
```

Activate the Hubot service on your ["Team Services"](http://my.slack.com/services/new/hubot) page inside Slack and
add the config variables. For example:

```sh
$ heroku config:add HUBOT_SLACK_TOKEN=xoxb-1234-5678-91011-00e4dd
```

Deploy and start the bot:

```sh
$ git push heroku master
$ heroku ps:scale web=1
```


### Slack adapter configuration

See `hubot-slack`'s [document](https://github.com/slackhq/hubot-slack).


Scripting
--------------------------------------------------------------------------------

### DIY

Take a look at the scripts in the `./scripts` folder for examples.
Delete any scripts you think are useless or boring.  Add whatever functionality you
want hubot to have. Read up on what you can do with hubot in the [Scripting Guide][scripting].

[scripting]: https://github.com/github/hubot/blob/master/docs/scripting.md


### hubot-scripts

Hubot has collection of [community scripts][hubot-scripts], but it is old.

Anyway, to enable scripts from the hubot-scripts package, add the script name with
extension as a double quoted string to the `hubot-scripts.json` file in this
repo.

[hubot-scripts]: https://github.com/github/hubot-scripts


### external-scripts

Want to maintain the repository and package yourself? Then this added functionality
maybe for you!

Hubot is now able to load scripts from [new community scripts](https://github.com/hubot-scripts)
or third-party `npm` packages! To enable this functionality you can follow
the following steps.

Add the packages as dependencies into your `package.json` like this:

```sh
$ npm i {package} --save
```

To enable third-party scripts that you've added you will need to add the package
name as a double quoted string to the `external-scripts.json` file in this repo.


Operation
--------------------------------------------------------------------------------

### Deployment

Push repository to Heroku:

```sh
$ git push heroku master
```

Or, if you want deploy this project to own heroku app, click the "Heroku Deploy" button:


### Restart the bot, watch logs

You may want to get comfortable with `heroku logs` and `heroku restart`
if you're having issues.

Restart:

```sh
$ heroku restart
```

tail:

```sh
$ heroku logs
```

Realtime monitoring:

```sh
$ heroku logs --tail
```

### Checking environment variables

Show environment variables:

```sh
$ heroku config
```

Export shell friendly:

```sh
$ heroku config --shell
```
