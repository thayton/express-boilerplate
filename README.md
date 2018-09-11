# Initialize package.json
    $ npm init -y

# Express

## Install express
    $ npm install express --save
    
## Handling Static Routes
Use the [express.static()](http://expressjs.com/en/starter/static-files.html) middleware to specify directory containing the static files:

```javascript
// file access at http://127.0.0.1:3000/style.css
app.use(express.static(__dirname + '/public'));

// file access at http://127.0.0.1:3000/public/style.css
app.use('/public', express.static(process.cwd() + '/public'));
```
## Using Handlebars Templating Engine

Install [hbs](https://www.npmjs.com/package/hbs)

    $ npm install hbs --save

Then configure express to use handlebars:

```javascript
const hbs = require('hbs');
app.set('view engine', 'hbs');
```

Create a `views/` sub-directory (`views/` is the default directory Express uses for templates)

    $ mkdir views
    
Use `res.render()` to inject variables into the hbs files:

```javascript
    res.render('about.hbs', {
        pageTitle: 'About Page',
        currentYear: new Date().getFullYear()
    });
```

`pageTitle` and `currentYear` can then be used within `about.hbs`:

```html
    <h1>{{ pageTitle }}</h1>
    <p>Some text here</p>
    <footer>
      <p>Copyright {{ currentYear }}</p>
    </footer>
```

To use partials, use `registerPartials` to specify the directory containing the partials:

```javascript
hbs.registerPartials(__dirname + '/views/partials');
```

Then, too include a partial (eg. `/views/partials/footer.hbs`) within an hbs file:

```javascript
{{> footer }}
```

Handlebars helpers can be used for common functions. For example:

```javascript
hbs.registerHelper('getCurrentYear', () => {
    return new Date().getFullYear();
});

hbs.registerHelper('screamIt', (text) => {
    return text.toUpperCase();
});
```

and then in the templates you can use `{{ getCurrentYear}}` or `{{ screamIt 'upper case me' }}`, or `{{ screamIt textVar }}` to run the functions.

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
