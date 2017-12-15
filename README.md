tar-files
---------

convenience wrapper around fs gunzip and node-tar to stream file entries' data.

```js
var te = require('tar-files')
var eos = require('end-of-stream')

// the first argument may be a file name or a readable stream.

te('package.tar',function(stream,cb){
  if(stream.path === "package/README.md") {
    eos(stream.pipe(fs.createWriteStream('./tar-README.md')),cb)
  } else {
    // skip this entry (make sure to call stream.resume() if skipping)
    stream.resume()
    cb()
  }
},function(err){
  
  // all done!

})

```

this example saves the `README.md` file from package.tar to the file `./tar-README.md`

- works with gzipped or not compressed tars.

- pass in a stream or a file name
