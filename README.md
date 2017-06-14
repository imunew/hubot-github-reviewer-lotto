# hubot-github-reviewer-lotto

## Run docker in local machine

### Requirement
- [docker community edition](https://www.docker.com/community-edition)

### Setup

#### Install hubot integration in your slack team

See https://slack.com/apps/A0F7XDU93-hubot

#### Clone repository

```bash
$ git clone git@github.com:imunew/hubot-github-reviewer-lotto.git
```

#### Create and edit .env file

```bash
$ cp docker/hubot/.env.example docker/hubot/.env
$ vi docker/hubot/.env
```

See https://github.com/sakatam/hubot-reviewer-lotto
- HUBOT_GITHUB_TOKEN
- HUBOT_GITHUB_ORG
- HUBOT_GITHUB_REVIEWER_TEAM
- HUBOT_GITHUB_WITH_AVATAR

See https://slackapi.github.io/hubot-slack/
- HUBOT_SLACK_TOKEN

See https://github.com/hubotio/hubot-redis-brain
- REDIS_URL

#### Build docker container

```bash
$ docker-compose build --no-cache
```

#### Run docker container

```bash
$ docker-compose up -d
```

### Assign a reviewer at random to pull-request

Move the slack channel that the hubot joined. 
And you can request a reviewer, like below.

```
#your-slack-channel
reviewer-bot reviewer for hubot-test 1
```

## Deploy hubot to heroku

### Requirement
- [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

### Setup
#### heroku login

```bash
$ heroku login
 ▸    heroku-cli: update available from 6.9.3-f709986 to 6.11.2-2aff95b
Enter your Heroku credentials:
Email: user@example.com
Password: ********
Logged in as user@example.com
```

#### heroku create

```bash
$ heroku create hubot-github-reviewer-lotto
  Creating ⬢ hubot-github-reviewer-lotto... done
  https://hubot-github-reviewer-lotto.herokuapp.com/ | https://git.heroku.com/hubot-github-reviewer-lotto.git
```

#### Install `Container Registry and Runtime` plugin

```bash
$ heroku plugins:install heroku-container-registry
Installing plugin heroku-container-registry... done
```

#### Log in to the Heroku container registry

```bash
$ heroku container:login
Login Succeeded
```

#### Push docker container

```bash
$ cd hubot
$ heroku container:push hubot
```

#### Configure environment variables

```bash
$ heroku config:set HUBOT_GITHUB_TOKEN={Input your github token}
$ heroku config:set HUBOT_GITHUB_ORG={Input your github organization}
$ heroku config:set HUBOT_GITHUB_REVIEWER_TEAM={Input your github reviewer team}
$ heroku config:set HUBOT_GITHUB_WITH_AVATAR={Input use avatar flag}
$ heroku config:set HUBOT_SLACK_TOKEN={Input your slack token}
```

#### Run docker container

```bash
$ heroku ps
Free dyno hours quota remaining this month: 1000h 0m (100%)
For more information on dyno sleeping and how to upgrade, see:
https://devcenter.heroku.com/articles/dyno-sleeping

=== hubot (Free): /bin/sh -c bin/hubot\ --adapter\ slack (1)
hubot.1: idle 2017/06/14 22:58:11 +0900 (~ 4s ago)
```

```bash
$ heroku ps:restart hubot
Restarting hubot dynos on ⬢ hubot-github-reviewer-lotto... done
```

```bash
$ heroku ps
Free dyno hours quota remaining this month: 1000h 0m (100%)
For more information on dyno sleeping and how to upgrade, see:
https://devcenter.heroku.com/articles/dyno-sleeping

=== hubot (Free): /bin/sh -c bin/hubot\ --adapter\ slack (1)
hubot.1: up 2017/06/14 22:59:55 +0900 (~ 7s ago)
```
