# change-private-gem-remotes-buildpack

A heroku buildpack for changing the repository urls as part of the application build.
It's meant to be used with [heroku-buildpack-multi](https://github.com/heroku/heroku-buildpack-multi),
before other buildpacks which require the urls to be replaced, like installing private `bundler` modules from `github`.

# Example usage

Upload the original and replacement urls to heroku.

``` sh-session
$ YOUR_OAUTH_KEY="INSERTYOUROAUTHKEYHERE"
$ heroku config:set ORIGINAL_REPO_URL="git@github.com:"
$ heroku config:set REPLACEMENT_REPO_URL="https:\/\/$YOUR_OAUTH_KEY:x-oauth-basic@github.com\/"
```

Use the Heroku Toolbelt to
[add this buildpack](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#adding-a-buildpack).
Use `--index` to make sure the buildpack runs before any others which might need
the replacements to be setup:

``` sh-session
$ heroku buildpacks:add --index 1 https://github.com/feedbackfruits/change-private-gem-remotes-buildpack.git
```
