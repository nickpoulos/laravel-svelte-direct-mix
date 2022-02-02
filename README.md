<p align="center"><img src="readme.jpg" width="75%"></p>

The companion Laravel Mix extension for Laravel Svelte Direct.

## Why?
The existing Svelte extension for Laravel Mix, determines which components to compile via a single entry point. This is how webpack itself operates and is totally standard. 

Svelte Direct looks to compile each Svelte component individually in a given directory, which allows each component to be loaded on its own when needed.

## Installation

You can install the package via npm or yarn:

```bash
npm install nickpoulos/laravel-svelte-direct-mix
```

## Usage

### Configure Laravel Mix
webpack.mix.js
```javascript
const mix = require('laravel-mix');
require('laravel-svelte-direct')

mix.svelteDirect('resources/js/Components', 'public/js');

```

### Example Configuring Additional Options (If Necessary, Default Shown)
webpack.mix.js
```javascript
const mix = require('laravel-mix');
require('laravel-svelte-direct-mix')

mix.svelteDirect(
    'resources/js/Components',
    'public/js',
    {
        componentMode: true,
        loaderOptions: {
            dev: !Mix.inProduction(),
            compilerOptions: {
                customElement: false
            }
        }
    }
);
```

Setting `componentMode: true` will build your components as typical Svelte components.  These can be loaded side by side as tiny Svelte applications on your page.  

Setting `componentMode: false` will build your components as WebComponents/customElements.  Doing so has certain caveats, including shadowDom, and some other quirks. For more information

`loaderOptions` gives full control over the Svelte Loader for Webpack. For more options check the [Svelte Loader](https://github.com/sveltejs/svelte-loader) package. 


For more information regarding Svelte and WebComponents, see the following resources:

- [https://dev.to/silvio/how-to-create-a-web-components-in-svelte-2g4j](https://dev.to/silvio/how-to-create-a-web-components-in-svelte-2g4j)
- [https://dev.to/richharris/why-i-don-t-use-web-components-2cia](https://dev.to/silvio/how-to-create-a-web-components-in-svelte-2g4j)
- Special shoutout to [Crisward](https://github.com/crisward/svelte-tag) and the awesome bootstrap code they wrote (provides the foundation for our boostrap code)


### Write Your Svelte Components

Write your Svelte components as your normally would, except for two small additions that we will add to the top of our file. Both are [part of the official Svelte docs/spec](https://svelte.dev/tutorial/svelte-options) and are not custom syntax.
```html
<!-- svelte-ignore missing-custom-element-compile-options -->
<svelte:options tag="flash-message" />
```
The options tag tells Svelte (and Svelte Direct), what the component's HTML tag should be. Normally this technique is only used in Svelte when compiling to WebComponents (more on that later). But it is the perfect mechanism for our cause as well.

The comment tag tells Svelte to ignore when we don't have `customElement` set to true.



### Planned Work

- [ ] Add tests.
- [ ] Allow for Blade within Svelte somehow? 


### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email **gal@wewowweb.com** instead of using the issue tracker.

## Credits

- [Crisward](https://github.com/crisward)
- [Gal Jakic](https://github.com/morpheus7CS)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
