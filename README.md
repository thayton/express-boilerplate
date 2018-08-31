# Deplying to Heroku

## Logging in
    $ heroku help
    $ heroku login

## Adding SSH keys
    $ heroku keys:add

## List SSH keys on account
    $ heroku keys

## Remove SSH keys on account
    $ heroku keys:remove

## Test SSH keys with Heroku
    $ ssh -v git@heroku.com

## Application Port

Set `port` to `process.env.PORT` in server.js to heroku can set the port for the application
using `process.env.PORT` environment variable.

## Package.json

Setup a `start` script in package.json for the Heroku to start the app:

    {
        ...
        "scripts": {
            "start": "node server/server.js"
            ...
        }
    }
    
This is necessary because Heroku doesn't know the name of the file to use to start the app.

## Push up application to Heroku

Run `heroku create` from within the application:

    $ heroku create

This will add a remote for Heroku:

    $ git remote -vv
    heroku	https://git.heroku.com/hidden-scrubland-50797.git (fetch)
    heroku	https://git.heroku.com/hidden-scrubland-50797.git (push)

Now use `git push` to push the application up to Heroku

    $ git push heroku master

To open the application in your web browser use:

    $ heroku open