{{#template name="GettingStarted"}}
First, you have to create a Meteor project:

```sh
meteor create myapp
```

Open the project's directory and add the Astronomy package.

```sh
cd myapp
meteor add jagi:astronomy
```

You're ready to go.

# Creating a first class

We'll start from showing the simplest possible class implementation.

```js
Posts = new Mongo.Collection('posts');

Post = Astro.Class({
  name: 'Post',
  collection: Posts
});
```

As you can see, we've created the Mongo collection named `Posts` and the `Post`  class. It's good to keep this convention. The `Posts` (plural) collection is a container for documents of the `Post` (singular) class. We've provided two attributes: `name` and `collection`. The `name` attribute is obligatory and it's just an internal name of the class. The `collection` attribute just tells our class in which collection instances of our class should be stored.

Now, we can create an instance of the `Post` class.

```js
var post = new Post();
```

Our class is very simple and right now doesn't make our lives easier. It doesn't have any fields, so let's change it.

```js
Post = Astro.Class({
  name: 'Post',
  collection: Posts,
  fields: {
    title: 'string',
    publishedAt: 'date'
  }
});
```

Now, we have the class with the two fields: `title` and `publishedAt`. The type of the `title` field is `string` and the type of the `publishedAt` field is `date`. Let's create an instance of the class and fill it with some values.

```js
var post = new Post({
  title: 'Sample title',
  publishedAt: new Date()
});
```

How to save the document into database? Nothing simpler.

```js
post.save();
```

Let's assume that after a while, we want to change the post's title.

```js
var post = Posts.findOne({title: 'Sample title'});
post.set('title', 'New title');
post.save();
```

In the listing above, we just fetch previously saved document and modified its title using the `set` function. After calling the `save` method only the title of the document will be updated in the database.

# Adding validation

Astronomy is highly modularized. By adding the `jagi:astronomy` package to your project you're only adding the basic functionalities. The validation feature is a separate module. To add it to the project you have to type in the console:

```sh
meteor add jagi:astronomy-validators
```

_NOTE: There's also the [Simple Validators](https://atmospherejs.com/jagi/astronomy-simple-validators) package that's much easier to use but has limited functionality._

Let's define some validation rules in our class.

```js
Post = Astro.Class({
  name: 'Post',
  collection: Posts,
  fields: {
    title: {
      type: 'string',
      validators: [
        Validators.minLength(3),
        Validators.maxLength(40)
      ]
    },
    publishedAt: 'date'
  }
});
```

We've modified the definition of the `title` field. Now instead passing a field type as a string, we pass an object. The object contains two properties: `type` and `validators`. The `type` property is just the type of the field. The `validators` property is a list of validators for the given field. We defined only two validators: `minLength` and `maxLength`. Now, we'll validate object before saving it.

```js
var post = new Post({
  /* ... */
});

if (post.validate()) {
  post.save();
}
```

The `validate` method will return false if any of the fields didn't pass validation rules.

# What next?

It was a brief introduction that covered only a tiny portion of Astronomy features. If you want to read more about Astronomy please take a look at the other sections in this documentation.

{{/template}}
