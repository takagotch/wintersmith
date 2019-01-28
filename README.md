### wintersmith
---
https://github.com/jnordberg/wintersmith

```
npm install wintersmith -g
wintersmith new <path>
cd <path>
wintersmith preview
wintersmith build
```

```
{
  "myfile.md": {MarkdownPlugin}
  "some-dir": {
    "image.jpg": {StaticPlugin}
    "random.file": {StaticPlugin}
  }
}

{
  "template": "template.pug",
  "stuff": {
    "things": 123,
    "moar": [1, 2, 3]
  }
}

```

```js
fs = require 'fs'
module.exports = (env, callback) ->
  class SimonSays extends env.ContentPlugin
    constructor: (@filepath, text) ->
      @text = "Simon syas: #{ text }"
    getFilename: -> @filepath.relative
    getView: -> (env, locals, conents, templates, callback) ->
      callback nullm newBuffer @text
  SimonSays.fromFile = (filepath, callback) ->
    fs.readFile filepath.full, (error, buffer) ->
      if error
        callback error
      else
        callback null, new SimonSays filepath, buffer.toString()
  env.registerContentPlugin 'text',
  callback()

var wintersmith = require('wintersmith');
var env = wintersmith('/path/to/my/config.json');
env.build(function(error){
  if(error) throw error;
  console.log('Done!');
});
env.preview(
  if(error) throw error;
  console.log('Server running!');
);
env.load(function(error, result){
  if(error) throw error;
  console.log('Contents loaded!');
});
```


