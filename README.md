# ember-query-params

Ember service for your query params

## Usage

```js
export default Ember.Controller.extend({
  paramsRelay: Ember.inject.service(),

  queryParams: [
    'theme',
    { isSidebarOpen: 'sidebar' }
  ],
  isSidebarOpen: false,
  theme: 'default',

  init() {
    this._super(...arguments);
    var paramsRelay = this.get('paramsRelay');

    paramsRelay.autoSubscribe(this);
    // or
    paramsRelay.subscribe('theme', (name, val) => {
      // name => 'theme'
      this.set(name, val);
    });
  }
});
```

In another place:

```js
export default Ember.Controller.extend({
  paramsRelay: Ember.inject.service(),

  actions: {
    toggleSidebar(val) {
      var paramsRelay = this.get('paramsRelay');

      paramsRelay.setParam('isSidebarOpen', val);
    }
  }
});
```

## Service API

- `setParam` - Function; For example `paramsRelay.setParam('name', value)`.
- `getParam` - Function; For example `paramsRelay.getParam('name')`. Returns the value, can be anything.
- `subscribe` - Function; For example `paramsRelay.subscribe('name', (key, value) => { //do something });`.
- `autoSubscribe` - Function; For example `paramsRelay.autoSubscribe(this)`. Where `this` is the controller that has a `queryParams` array.
  All query params must have a unique name, since setting a 'theme' in one controller will set the same QP in another.

## Custom Service

You can also setup your own service, just use the mixin.

```js
import Ember from 'ember';
import QPMixin from 'ember-query-params/mixins/query-params';

export default Ember.Service.extend(QPMixin, {
  // your code
});
```

## Contributing

See [CONTRIBUTING.md].

[CONTRIBUTING.md]: CONTRIBUTING.md
