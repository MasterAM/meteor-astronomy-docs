{{#template name="Behaviors"}}
Built in behaviors module is a nice way of reusing your code. If you have similar features in two or more classes, you should consider creating a behavior for that. An example of a good behavior can be `createdAt` and `updateAt` fields which should be filled with the current date on document save and on every document update. And it's why we've created the `timestamp` behavior for that purpose. In this section, we will discuss all official behaviors.

**Adding behavior to the class**

We add behaviors to the class by providing their names and options under the `behaviors` property in the class definition. We have two ways of specifying behaviors:

1. An array of behavior names, which sets the default options for each behavior.
2. An object with behavior names as keys and options as values.

Let's see both ways of defining them.

```js
User = Astro.Class({
  name: 'User',
  /* ... */
  behaviors: ['timestamp']
});
```

You can also pass options to the behavior.

```js
User = Astro.Class({
  name: 'User',
  /* ... */
  behaviors: {
    timestamp: {
      createdFieldName: 'created'
    }
  }
});
```
{{/template}}
