{{#template name="Slug"}}
You can add the `slug` behavior to your project by executing the following command.

```sh
meteor add jagi:astronomy-slug-behavior
```

The `slug` behavior adds a slug field for storing an URL friendly value of a chosen field. The slug field can be used in the routing for generating URLs `http://localhost:3000/post/to-jest-test-polskich-znakow-aszclonz`.

The `slug` behavior comes with following options.

```js
behaviors: {
  slug: {
    // The field name from which a slug will be created.
    fieldName: 'title',
    // The field name where a slug will be stored.
    slugFieldName: 'slug',
    // A flag indicating if we can update a slug.
    canUpdate: true,
    // A flag indicating if a slug is unique.
    unique: true,
    // A separator used for generating a slug.
    separator: '-'
  }
}
```

Let's take a look at the behavior usage.

```js
var post = new Post();
post.title = 'To jest test polskich znaków ąśźćłóńż';
post.save();

post.slug; // "to-jest-test-polskich-znakow-aszclonz"
```
{{/template}}
