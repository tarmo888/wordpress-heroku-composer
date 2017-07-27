Use Heroku Button or Bash commands for deploying.

## Deploy via Heroku Button

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Deploy via Bash command line

```bash
mkdir new-app-folder
cd new-app-folder
git clone https://github.com/tarmo888/wordpress-heroku-composer.git .
```

Login to Heroku and create new app.
```bash
heroku login
heroku apps:create new-app-name --buildpack heroku/php --region eu
```

Add the following add-ons.
```bash
heroku addons:add jawsdb-maria:kitefin
heroku addons:add heroku-redis:hobby-dev
heroku addons:add sendgrid:starter
heroku addons:add papertrail:choklad
heroku addons:add scheduler:standard
```

Set your AWS credentials.
```bash
heroku config:set AWS_ACCESS_KEY_ID=
heroku config:set AWS_SECRET_ACCESS_KEY=
```

Disable WP Cron to call it from Scheduler instead? (0 or 1).
If you set DISABLE_WP_CRON=1 then add this to Heroku Scheduler for every 10 minutes: "php /app/cms/wp-cron.php"
```bash
heroku config:set DISABLE_WP_CRON=0
```

Force login and admin to HTTPS? (0 or 1)
```bash
heroku config:set FORCE_SSL=0
```

Visit Wordpress hash generator and set following values
https://api.wordpress.org/secret-key/1.1/salt/
```bash
heroku config:set AUTH_KEY=
heroku config:set SECURE_AUTH_KEY=
heroku config:set LOGGED_IN_KEY=
heroku config:set NONCE_KEY=
heroku config:set AUTH_SALT=
heroku config:set SECURE_AUTH_SALT=
heroku config:set LOGGED_IN_SALT=
heroku config:set NONCE_SALT=
```

Deploy your app to Heroku.
```bash
git add .
git commit -am "init"
git push heroku master
```