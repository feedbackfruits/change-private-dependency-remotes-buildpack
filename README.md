# change-private-dependency-remotes-buildpack

A heroku buildpack for changing the repository urls as part of the application build.
It's meant to be used with [heroku-buildpack-multi](https://github.com/heroku/heroku-buildpack-multi),
before other buildpacks which require the urls to be replaced, like installing private `pip` modules from `github`.

Can be used for any dependency manager, but defaults to `pip` standards.

# Configuration
Environment variabes with defaults:
```
DEPENDENCY_FILES="requirements.txt"
ORIGINAL_REPO_URL="ssh:\/\/git@github.com\/"
REPLACEMENT_REPO_URL="https:\/\/$GITHUB_OAUTH_KEY:x-oauth-basic@github.com\/" # Requires GITHUB_OAUTH_KEY to be specified
```
Note, the last two must be escaped for use in `sed`

# Example usage

Upload the original and replacement urls to heroku.

``` sh-session
$ heroku config:set YOUR_OAUTH_KEY="INSERTYOUROAUTHKEYHERE"
```

Use the Heroku Toolbelt to
[add this buildpack](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#adding-a-buildpack).
Use `--index` to make sure the buildpack runs before any others which might need
the replacements to be setup:

``` sh-session
$ heroku buildpacks:add --index 1 https://github.com/feedbackfruits/change-private-dependency-remotes-buildpack.git
```
