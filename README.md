# Ghost-Json

A Ghost theme that delivers JSON data instead of HTML.  
Intended use case: using Ghost as a data backend, e.g. for an app.

## Getting this

git clone/submodule this repo.

## Requirements

none, so far

## The idea

Ghost delivers static (HTML) content rendered from the Handlebars templates
contained in a theme.  
Since HTML is text, we can technically output another format.  
So, if we were to create handlebars templates to pour out JSON content, we could load this
JSON data into another client (e.g. AngluarJS) and render it there.

## Status

- index outputs all content. useful to get 1 big JSON for an app.
- post outputs content for 1 post.
- tag outputs data for given tag.
- author outputs data for given author.

The JSON format is not final, and heavily depends on the client-side usage.

## The bigger idea

Imagine you have an app (written in IonicJS/AngularJS),
that loads its content as JSON data on startup.
Now, there are plenty of backend services you could run, but with varying complexity.
Having to keep it simple so that non-tech people can change the content in a simple way,
one solution is to make the content blog-like.

The use-case for out solution:
- we have an IonicJS app running on mobile devices,
- it uses a Ghost-blog as backend, since it's simple to deploy (via GhostPro, Heroku or self-hosting)
and can be run locally for debugging.
