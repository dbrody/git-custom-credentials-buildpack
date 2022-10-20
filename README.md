# git-custom-credentials-buildpack

This is to use git credentials in buildpacks to load private repositories.

This repo is bash scripts so there are no dependencies such as ruby.

## Usage

Set the environment variable `GIT_ACCESS_CREDENTIALS` to a list of credentials you want to use.

The format of the credentials should be of the format specified by `git config credential` [here](https://git-scm.com/docs/git-credential-store#_storage_format).

You may use multiple credentials by splitting them with a commad `,` in `GIT_ACCESS_CREDENTIALS`.

An example credential should be of the format such as: `https://x-oauth-basic:<GITHUB_ACCESS_TOKEN>@github.com/`


## Why?

Most alternatives seem to be old or have dependencies.

Alternative [custom-ssh-key-buildpack](https://github.com/simon0191/custom-ssh-key-buildpack) requires ruby which is not available by default on Heroku stack 22.

One alternative is [heroku-buildpack-github-netrc](https://github.com/timshadel/heroku-buildpack-github-netrc.git) but this doesnt properly set environment for fetching private repos during application build for some reason.


## Use case

My main use case for this is it allows for elixir applications to download private repositories on deployment.

In your `mix.exs` file you can include a private repo just like any other repository:
```elixir
...
deps: [
    ...,
    {:some_private_repo, github: "username/private-repo", tag: "0.6.11"}
]
```

Just add a credential with an access token with read content permissions to your private repository.