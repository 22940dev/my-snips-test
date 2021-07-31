## Usage

This library is a tiny wrapper around [github-base](https://github.com/jonschlinkert/github-base), see that project's readme for more information about available options and authentication choices.

**Params**

* `users` **{String|Array}**: One or more users or organization names.
* `options` **{Object}**: See available [options](#options).
* `returns` **{Promise}**

**Example**

```js
const repos = require('repos');
const options = {
  // see github-base for other authentication options
  token: 'YOUR_GITHUB_AUTH_TOKEN'
};
repos(['doowb', 'jonschlinkert'], options)
  .then(function(repos) {
    // array of repository objects
    console.log(repos);
  })
  .catch(console.error)
```

See the [GitHub API documentation for repositories](https://developer.github.com/v3/repos/) for more details about the objects returned for each repository.

## Options

| **Option** | **Type** | **Default** | **Description** | 
| --- | --- | --- | --- |
| `filterOrgs` | `function` | undefined | Function for filtering organizations from the result. |
| `filterRepos` | `function` | undefined | Function for filtering repositories from the result. |
| `sort` | `boolean` | `true` | By default, the returned list is sorted by repository `name` |
