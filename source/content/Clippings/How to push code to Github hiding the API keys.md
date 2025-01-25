---
title: "How to push code to Github hiding the API keys?"
source: "https://stackoverflow.com/questions/44342276/how-to-push-code-to-github-hiding-the-api-keys"
author:
  - "[[Stack Overflow]]"
published: 2017-06-03
created: 2025-01-25
description: "I want to push some codes to my GitHub Repository. These codes are in different languages like Javascript, Java, Python etc. Some of those codes contain some private API key that I don't want to pu..."
tags:
  - "clippings"
---
Any time you have files with sensitive data like

```
config.yml
```

you MUST NOT commit them to your repository. I'll show you an example.

Suppose you have a yaml file with some username and password:

```
# app/config/credentials.yml
credentials:
    username: foo
    password: bar
```

If you want to hide the `foo` and the `bar` values, remove this file from your repository, but add a `distribution` file that aims to maintain username and password fields, but without any real values:

```
# app/config/credentials.yml.dist
credentials:
    username: ~
    password: ~
```

During installation you can get this file by copying `app/config/credentials.yml.dist` to `app/config/credentials.yml`.

Also, remember to add `app/config/credentials.yml` to your `.gitignore` file.

Its the same with api keys:

```
# app/config/config.yml
config:
    credentials:
        username: foo
        password: bar
    api_stuffs:
        api_foo: fooooo
        api_secret: baaaaar
        api_token: tooooken
```

This works well for configuration files, and is a good pattern that saves you every time you need to share the structure of a configuration but not sensitive data. Init files, configurations and so on.