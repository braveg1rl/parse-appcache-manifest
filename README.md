# parse-appcache-manifest [![Build Status](https://travis-ci.org/meryn/parse-appcache-manifest.png?branch=master)](https://travis-ci.org/meryn/parse-appcache-manifest) [![Dependency Status](https://david-dm.org/meryn/parse-appcache-manifest.png)](https://david-dm.org/meryn/parse-appcache-manifest)

Parses HTML5 application cache manifest.

## Usage

```javascript
parseManifest = require("parse-appcache-manifest")
entries = parseManifest(manifest)
```

`entries` will be an object with three properties: `cache`, `network`, `fallback`. 

`cache` and `network` are both arrays which contain entries. 

`fallback` is an object with the url (or url pattern) as key, and the fallback url as value.


If you need access to a tokenized version of the manifest file (e.g., you want to modify an existing manifest file and need to preserve comments and newlines, etc)


```coffeescript
appcacheParse  = require 'parse-appcache-manifest'
result = appcacheParse(input).tokens
```

where `result` is a flat, ordered list of tokens that comes back. 

 `input` =

```
CACHE MANIFEST

# some explicit resources
CACHE:
/happy.html
/good.css

NETWORK:
*
http://*
https://*
```

`result` =

```json
[
  { type: 'magic signature', value: 'CACHE MANIFEST' },
  { type: 'newline' },
  { type: 'comment', value: 'some explicit resources' },
  { type: 'mode', value: 'CACHE' }
  { type: 'data', tokens: [ '/happy.html' ] },
  { type: 'data', tokens: [ '/good.css' ] },
  { type: 'newline' },
  { type: 'mode', value: 'NETWORK' }
  { type: 'data', tokens: [ '*' ] },
  { type: 'data', tokens: [ 'http://*' ] },
  { type: 'data', tokens: [ 'https://*' ] }
]
```

You can use https://github.com/meryn/render-appcache-manifest to convert a token list back to an appcache manifest.

## Credits

The initial structure of this module was generated by [Jumpstart](https://github.com/meryn/jumpstart), using the [Jumpstart Black Coffee](https://github.com/meryn/jumpstart-black-coffee) template.

This code is based on code from [Mikko Ohtamaa](http://opensourcehacker.com/).

## License

parse-appcache-manifest is released under the [MIT License](http://opensource.org/licenses/MIT).  
Copyright (c) 2013 Meryn Stol  