{{#template name="TransientFields"}}
Some fields may be computed from the values of other fields instead of being persisted in the database. A good example is calculating a person's age from a birth date. While age changes during the time, the birth date is constant, so it's why we should only store the birth date. The example below shows how to set the `age` field as transient and calculate its value.

*NOTE: To calculate the age from the birth date we used the `afterInit` event. You will learn more about events in the following sections of this documentation.*

```js
User = Astro.Class({
  name: 'User',
  /* ... */
  fields: {
    birthDate: 'date',
    age: {
      type: 'number',
      transient: true
    }
  },
  events: {
    afterInit: function() {
      var birthDate = this.birthDate;
      if (birthDate) {
        var diff = Date.now() - birthDate.getTime();
        this.set('age', Math.abs((new Date(diff)).getUTCFullYear() - 1970));
      }
    }
  }
});
```
{{/template}}
