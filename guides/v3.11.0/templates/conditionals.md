Statements like [`if`](https://api.emberjs.com/ember/3.11/classes/Ember.Templates.helpers/methods/if?anchor=if)
and [`unless`](https://api.emberjs.com/ember/3.11/classes/Ember.Templates.helpers/methods/if?anchor=unless)
are implemented as built-in helpers. Helpers can be invoked three ways, each
of which is illustrated below with conditionals.

The first style of invocation is **inline invocation**. This looks similar to
displaying a property, but helpers accept arguments. For example:

```handlebars
<div>
  {{if this.isFast "zoooom" "putt-putt-putt"}}
</div>
```

[`{{if}}`](https://api.emberjs.com/ember/3.11/classes/Ember.Templates.helpers/methods/if?anchor=if)
in this case returns `"zoooom"` when `isFast` is true and
`"putt-putt-putt"` when `isFast` is false. Helpers invoked as inline expressions
render a single value, the same way that properties are a single value.

Inline helpers don't need to be used inside HTML tags. They can also be used
inside attribute values:

```handlebars
<div class="is-car {{if this.isFast "zoooom" "putt-putt-putt"}}">
</div>
```

**Nested invocation** is another way to use a helper. Like inline helpers,
nested helpers generate and return a single value. For example, this template
only renders `"zoooom"` if both `isFast` and `isFueled` are true:

```handlebars
<div>
  {{if this.isFast (if this.isFueled "zoooom")}}
</div>
```

The nested helper is called first returning `"zoooom"` only if `isFueled` is
true. Then the inline expression is called, rendering the nested helper's
value (`"zoooom"`) only if `isFast` is true.

The third form of helper usage is **block invocation**. Use block helpers
to render only part of a template. Block invocation of a helper can be
recognized by the `#` before the helper name, and the closing `{{/` double
curly brace at the end of the invocation.

For example, this template conditionally shows
properties on `person` only if that it is present:

```handlebars
{{#if this.person}}
  Welcome back, <b>{{this.person.firstName}} {{this.person.lastName}}</b>!
{{/if}}
```

[`{{if}}`](https://api.emberjs.com/ember/3.11/classes/Ember.Templates.helpers/methods/if?anchor=if)
checks for truthiness, which means all values except `false`,
`undefined`, `null`, `''`, `0`  or `[]` (i.e., any JavaScript falsy value or an
empty array).

If a value passed to `{{#if}}` evaluates to falsy, the `{{else}}` block
of that invocation is rendered:

```handlebars
{{#if this.person}}
  Welcome back, <b>{{this.person.firstName}} {{this.person.lastName}}</b>!
{{else}}
  Please log in.
{{/if}}
```

`{{else}}` can chain helper invocation, the most common use case for this being
`{{else if}}`:

```handlebars
{{#if this.isAtWork}}
  Ship that code!
{{else if this.isReading}}
  You can finish War and Peace eventually...
{{/if}}
```

The inverse of `{{if}}` is
[`{{unless}}`](https://api.emberjs.com/ember/3.11/classes/Ember.Templates.helpers/methods/if?anchor=unless),
which can be used in the same three styles of invocation. For example, this
template only shows an amount due when the user has not paid:

```handlebars
{{#unless this.hasPaid}}
  You owe: ${{this.total}}
{{/unless}}
```
