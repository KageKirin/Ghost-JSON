# Ghost-Json

A Ghost theme that delivers JSON data instead of HTML.  
Intended use case: using Ghost as a data backend, e.g. for an app.

Ghost version 0.7.2 exposes a RESTful API (see [Ghost public API v0.1](https://api.ghost.org/v0.1/docs)),
but this API is not (or hardly) accessible from outside of Ghost's server context.

Hence this theme, which outputs pretty much the same information as Ghost's API,
in the same JSON format as Ghost itself.


## Getting this

git clone/submodule this repo.

## Requirements

Ghost, version 0.7.2 for the API access

## The idea

Ghost delivers static (HTML) content rendered from the Handlebars templates
contained in a theme.  
Since HTML is text, we can technically output another format.  
So, if we were to create handlebars templates to pour out JSON content, we could load this
JSON data into another client (e.g. AngluarJS) and render it there.

## Status

Ghost API v0.1 completely mapped, with some additions.
The Handlebars templates are relying on the `{{#get}}` helper to access the data.

### Index

Returns a collection of all [posts](https://api.ghost.org/docs/post), [tags](https://api.ghost.org/docs/post) and [users](https://api.ghost.org/docs/user).

Query format: `http://a-ghost-blog.com/`

```
{
	"posts":[{
		"id":1,
		"uuid":"bc0a0924-b49c-45c8-897d-728f6acba7c9",
		"title":"Welcome to Ghost",
		"slug":"welcome-to-ghost",
		"markdown":"*cut for sanity*",
		"html":"<p>*cut for sanity*</p>",
		"image":null,
		"featured":false,
		"page":false,
		"status":"published",
		"language":"en_US",
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1,
		"published_at":"2014-11-17T19:02:27.173Z",
		"published_by":1,
		"author":1,
		"url":"/welcome-to-ghost/"
	} /*,{etc}*/
	],

	"tags":[{
		"id":1,
		"uuid":"ec3a0924-a59c-45c8-817d-428f6acba7c4",
		"name":"Getting Started",
		"slug":"getting-started",
		"hidden": false,
		"parent": null,
		"image":null,
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1
	} /*,{etc}*/
	],

	"users":[{
		"accessibility": null,
		"bio": null,
		"cover": null,
		"created_at": "2014-10-11T19:02:27.147Z",
		"created_by": 1,
		"id":1,
		"image": null,
		"language": "en_US",
		"last_login": "2014-11-17T19:02:27.147Z",
		"location": null,
		"meta_description": null,
		"meta_title": null,
		"name": "Eric Almeida",
		"slug": "eric-almeida",
		"status":"active",
		"tour": null,
		"updated_at":"2014-10-11T19:02:27.147Z",
		"updated_by":1,
		"uuid": "fs4a0021-b22a-33a1-531c-424e2caba3c3",
		"website": null,
	} /*,{etc}*/
	],

	"meta":{
		"pagination":{
			"page":1,
			"limit":2,
			"pages":1,
			"total":1,
			"next":null,
			"prev":null
		}
	}
```

The meta object is a placeholder filled with static data.


### Post

**CAVEAT**: post.html and post.markdown are encoded via Ghost's `encode` filter.

Returns the given post.

Query format: `http://a-ghost-blog.com/:post.slug/`.
E.g. `http://a-ghost-blog.com/welcome-to-ghost/`.

**trailing slash matters!**

```
{
	"posts":[{
		"id":1,
		"uuid":"bc0a0924-b49c-45c8-897d-728f6acba7c9",
		"title":"Welcome to Ghost",
		"slug":"welcome-to-ghost",
		"markdown":"*cut for sanity*",
		"html":"<p>*cut for sanity*</p>",
		"image":null,
		"featured":false,
		"page":false,
		"status":"published",
		"language":"en_US",
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1,
		"published_at":"2014-11-17T19:02:27.173Z",
		"published_by":1,
		"author":1,
		"url":"/welcome-to-ghost/"
	}
	],

	"meta":{
		"pagination":{
			"page":1,
			"limit":2,
			"pages":1,
			"total":1,
			"next":null,
			"prev":null
		}
	}
```


### Tag

Returns the given tag AND a list of associated posts.

Query format: `http://a-ghost-blog.com/tag/:tag.slug/`.
E.g. `http://a-ghost-blog.com/tag/getting-started/`.

**trailing slash matters!**


```
{
	"tags":[{
		"id":1,
		"uuid":"ec3a0924-a59c-45c8-817d-428f6acba7c4",
		"name":"Getting Started",
		"slug":"getting-started",
		"hidden": false,
		"parent": null,
		"image":null,
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1
	}
	],

	"posts":[{
		"id":1,
		"uuid":"bc0a0924-b49c-45c8-897d-728f6acba7c9",
		"title":"Welcome to Ghost",
		"slug":"welcome-to-ghost",
		"markdown":"*cut for sanity*",
		"html":"<p>*cut for sanity*</p>",
		"image":null,
		"featured":false,
		"page":false,
		"status":"published",
		"language":"en_US",
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1,
		"published_at":"2014-11-17T19:02:27.173Z",
		"published_by":1,
		"author":1,
		"url":"/welcome-to-ghost/"
	} /*,{etc}*/
	],

	"meta":{
		"pagination":{
			"page":1,
			"limit":2,
			"pages":1,
			"total":1,
			"next":null,
			"prev":null
		}
	}
```

### User/Author

Returns the given user AND a list of associated posts.

Query format: `http://a-ghost-blog.com/author/:user.slug/`.
E.g. `http://a-ghost-blog.com/author/me/`.

**trailing slash matters!**

```
{
	"users":[{
		"accessibility": null,
		"bio": null,
		"cover": null,
		"created_at": "2014-10-11T19:02:27.147Z",
		"created_by": 1,
		"id":1,
		"image": null,
		"language": "en_US",
		"last_login": "2014-11-17T19:02:27.147Z",
		"location": null,
		"meta_description": null,
		"meta_title": null,
		"name": "Eric Almeida",
		"slug": "eric-almeida",
		"status":"active",
		"tour": null,
		"updated_at":"2014-10-11T19:02:27.147Z",
		"updated_by":1,
		"uuid": "fs4a0021-b22a-33a1-531c-424e2caba3c3",
		"website": null,
	} /*,{etc}*/
	],

	"posts":[{
		"id":1,
		"uuid":"bc0a0924-b49c-45c8-897d-728f6acba7c9",
		"title":"Welcome to Ghost",
		"slug":"welcome-to-ghost",
		"markdown":"*cut for sanity*",
		"html":"<p>*cut for sanity*</p>",
		"image":null,
		"featured":false,
		"page":false,
		"status":"published",
		"language":"en_US",
		"meta_title":null,
		"meta_description":null,
		"created_at":"2014-11-17T19:02:27.147Z",
		"created_by":1,
		"updated_at":"2014-11-17T19:02:27.147Z",
		"updated_by":1,
		"published_at":"2014-11-17T19:02:27.173Z",
		"published_by":1,
		"author":1,
		"url":"/welcome-to-ghost/"
	} /*,{etc}*/
	],

	"meta":{
		"pagination":{
			"page":1,
			"limit":2,
			"pages":1,
			"total":1,
			"next":null,
			"prev":null
		}
	}
```


## The bigger idea

Imagine you have an app (written in IonicJS/AngularJS),
that loads its content as JSON data on startup.
Now, there are plenty of backend services you could run, but with varying complexity.
Having to keep it simple so that non-tech people can change the content in a simple way,
one solution is to make the content blog-like.

The use-case for our solution:
- we have an IonicJS app running on mobile devices,
- it uses a Ghost-blog as backend, since it's simple to deploy (via GhostPro, Heroku or self-hosting)
and can be run locally for debugging.
