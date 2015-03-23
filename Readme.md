# Helpers for [FlowRouter](https://github.com/meteorhacks/flow-router/)

Template helpers for meteorhacks:flow-router

- isSubReady
- isActivePath
- isNotActivePath
- pathFor (still under development)

### Install
```sh
meteor add arillo:flow-router-helpers
```

### Usage isSubReady

Checks whether your subscription is ready. If you don't pass a subscription name it will check for all subscriptions.

```html
{{#if isSubReady 'items'}}
	<ul>
	{{#each items}}
		<li>{{title}}</li>
	{{/each}}
	</ul>
{{/if}}
```

### Usage isActivePath

`isActivePath` returns the string `active` or boolean `false` unless you specify `className` then this string is returned instead of `active`.

`isNotActivePath` returns the string `disabled` or boolean `false` unless you specify `className` then this string is returned instead of `disabled`.

```html
<nav>
  <ul>
    <li class="{{isActivePath regex='users' className='on'}}">...</li>
    <li class="{{isActivePath regex='products'}}">...</li>
    {{#if isActivePath regex='index'}}
      <li>...</li>
    {{/if}}
    <li class="{{isNotActivePath regex='dashboard'}}">...</li>
  </ul>
</nav>
```
This helper uses regex which means strings like this will work too.
```js
'^dashboard$' // Exact match for 'dashboard'
'^product' // Begins with 'product'
'list$' // Ends with 'list'
```
* We used [iron-router-active](https://github.com/zimme/meteor-iron-router-active/)
as an inspiration and refactored it to work with flow-router


### Usage pathFor

Used to build a path to your route. (Still in active development)
We have to consider how to pass queryParameters to the helper.

```html
<a href="{{pathFor '/post/:id' id=_id}}">Link to post</a>
<a href="{{pathFor '/post/:id/comments/:cid' id=_id cid=comment._id}}">Link to comment in post</a>
```