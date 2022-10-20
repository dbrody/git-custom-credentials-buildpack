# github-access-token-buildpack

This is to use git credentials in buildpacks to load private repositories.
This repo is bash scripts so there are no dependencies such as ruby.

## Usage

Set the environment variable `GIT_ACCESS_CREDENTIALS` to a list of credentials you want to use.

The format of the credentials should be of the format specified by `git config credential` [here](https://git-scm.com/docs/git-credential-store#_storage_format).

You may use multiple credentials by splitting them with a commad `,` in `GIT_ACCESS_CREDENTIALS`.


## Why?

One alternative is [heroku-buildpack-github-netrc](https://github.com/timshadel/heroku-buildpack-github-netrc.git) but this doesnt properly set environment for fetching private repos during application build for some reason.

Alternative [custom-ssh-key-buildpack](https://github.com/simon0191/custom-ssh-key-buildpack) requires ruby which is not available by default on Heroku stack 22.