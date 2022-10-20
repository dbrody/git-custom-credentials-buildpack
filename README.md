# git-custom-credentials-buildpack

This allows adding git credentials in buildpacks to load private repositories.

## Installation

Add buildpack at the beginning so it runs before your app is build:

`heroku buildpacks:add -i 1 https://github.com/dbrody/git-custom-credentials-buildpack`

Set your credentials:

`heroku config:set GIT_ACCESS_CREDENTIALS=https://x-oauth-basic:<GITHUB_ACCESS_TOKEN>@github.com/`

Replace `<GITHUB_ACCESS_TOKEN>` with your actual token.


## Usage

Set the environment variable `GIT_ACCESS_CREDENTIALS` to a list of credentials you want to use.

The format of the credentials should be of the format specified by `git config credential` [here](https://git-scm.com/docs/git-credential-store#_storage_format).

You may use multiple credentials by splitting them with a commad `,` in `GIT_ACCESS_CREDENTIALS`.

An example credential should be of the format such as: `https://x-oauth-basic:<GITHUB_ACCESS_TOKEN>@github.com/`


## Why?

Most alternatives seem to be old or have dependencies.

[custom-ssh-key-buildpack](https://github.com/simon0191/custom-ssh-key-buildpack) requires ruby which is not available by default on Heroku stack 22.

[heroku-buildpack-github-netrc](https://github.com/timshadel/heroku-buildpack-github-netrc.git) but the repository is old and doesnt properly set environment for fetching private repos during application build for some reason.

## Use case

My main use case for is for elixir applications to download private repositories on deployment.

In a `mix.exs` file you can include a private repo just like any other repository:
```elixir
...
deps: [
    ...,
    {:some_private_repo, github: "username/private-repo", tag: "0.6.11"}
]
```

Just add a credential with an access token with read content permissions to your private repository.