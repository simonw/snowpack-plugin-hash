# snowpack-plugin-hash

Snowpack integration for [@typed/content-hash](https://github.com/TylorS/typed-content-hash) to apply content hashes to all of your build assets. This can be helpful in production to allow caching files permanently since the hashes are determinstic based on the contents of the file.

Note that this plugin uses Snowpack's "optimize" plugin API which will only run during `snowpack build` to prepare your assets for production.

## Features

- SHA-512 Content Hashes for JS, JSX, and CSS files, and their dependencies!.
- SourceMap generation w/ remapping support
- Remaps `import-map.json` to reference hashes
- Generates an asset manifest for all files
- Rewrites all the `script.src` and `link.href` in your HTML files.
- Supports Snowpack v3 API

## Install

```sh
npm i --save-dev snowpack-plugin-hash

yarn add -d snowpack-plugin-hash
```

## Usage

So far in my experience it has been best to keep this plugin last to ensure the asset manifest is correct.

```js
// snowpack.config.js

module.exports = {
  ...config,
  plugins: [
    [
      'snowpack-plugin-hash',
      // Entirely optional object. Showing default values
      { 
        // Name of custom tsconfig to use for compiler options passed to TypeScript compiler
        readonly tsConfig?: undefined
        // Configured length of your hashes
        readonly hashLength?: number
        // Name of file for asset manifest JSON
        readonly assetManifest?: string
        // BaseURL to use to rewrite files being hashed
        readonly baseUrl?: string
      }
    ]
  ]
}
```