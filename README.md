# Ghost Qiniu Storage

This [Ghost custom storage module](https://github.com/TryGhost/Ghost/wiki/Using-a-custom-storage-module) allows you to store media file at [Qiniu](http://www.qiniu.com/) instead of storing at local machine. It requires Ghost greater than `0.6.0`!

## Installation

### Via NPM

- Install Qiniu storage module

  ```
  npm install ghost-qn-store
  ```
- Make the storage folder if it doesn't exist yet

  ```
  mkdir content/storage
  ```
- Copy the module into the right location

  ```
  cp -vR node_modules/ghost-qn-store content/storage/qn-store
  ```

### Via Git

In order to replace the storage module, the basic requirements are:

- Create a new folder inside `/content` called `/storage`

- Clone this repo to `/storage`

  ```
  cd [path/to/ghost]/content/storage
  git clone https://github.com/Minwe/qn-store.git
  ```

- Install dependencies

  ```
  cd qn-store
  npm install
  ```

  You can add `qn` to dependencies in Ghost's `package.json`.

### The Old way

**The instruction below is NOT recommended for upgrade reason：**

> Your install instructions require users to do an `npm install --save` - this modifies the package.json and makes the upgrade path for Ghost much, much harder. This was never the intention with the storage system. ([via](https://github.com/minwe/qn-store/issues/6))

- **Installation from NPM.**
  
  ``` 
  npm install --save ghost-qn-store
  ```
  
- **Create storage module.**
  
  Create `index.js` file with folder path `content/storage/qn-store/index.js` (manually create folder if not exist).
  
  ``` javascript
  'use strict';
  
  module.exports = require('ghost-qn-store');
  
  ```

## Configuration

In your `config.js` file, you'll need to add a new `storage` block to whichever environment you want to change:

``` js
storage: {
  active: 'qn-store',
  'qn-store': {
    accessKey: 'your access key',
    secretKey: 'your secret key',
    bucket: 'your bucket name',
    origin: 'http://xx.xx.xx.glb.clouddn.com',
    // timeout: 3600000, // default rpc timeout: one hour, optional
    // if your app outside of China, please set `uploadURL` to `http://up.qiniug.com/`
    // uploadURL: 'http://up.qiniu.com/'
    filePath: 'YYYY/MM/' // default `YYYY/MM/`, will be formated by moment.js, using `[]` to escape
  }
}
```

## License

Read [LICENSE](LICENSE)
