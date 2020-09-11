<div align="center">

# Ckan-client-js

[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/datopian/ckan-client-js/issues)
![build](https://github.com/datopian/ckan-client-js/workflows/ckan-client-js%20actions/badge.svg)
[![The MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](http://opensource.org/licenses/MIT)


Ckan-client-js is a "SDK" in javascript for uploading files and updating metastore.<br> This SDK will communicate with [Ckanext-authz-service](https://github.com/datopian/ckanext-authz-service)(Use CKAN to provide authorization tokens for other related systems
), [giftless service](https://github.com/datopian/giftless)(A highly customizable and extensible Git LFS server implemented in Python
) and uploading to Blob storage.

</div>

## Prerequisites

- [Node](https://nodejs.org/en/)
- [NPM Package Manager](https://www.npmjs.com/)

## Built with

- [crypto-js](https://cryptojs.gitbook.io/docs/)
- [axios](https://github.com/axios/axios)
- [ava](https://github.com/avajs/ava)
- [nock](https://github.com/nock/nock)
- [webpack](https://webpack.js.org/)

## Install

First, clone the repo via git:

```bash
$ git clone git@github.com:datopian/ckan-client-js.git
```

And then install dependencies with npm.

```bash
$ cd ckan-client-js
```

```bash
$ npm install
```

It will create a directory called `ckan-client-js`.<br>
Inside that directory, it will generate the initial project structure.

```bash
ckan-client-js
.
├── CHANGELOG.md
├── CONTRIBUTING.md
├── lib
│   ├── file.js
│   ├── index.js
│   └── util
│       ├── ckan-auth-api.js
│       └── ckan-upload-api.js
├── License
├── package.json
├── package-lock.json
├── README.md
├── test
│   ├── fixtures
│   │   └── sample.csv
│   └── upload.test.js
└── webpack.config.js
```

## Use

Upload file from **NodeJS**

```js
const { Client, Open } = require('./lib/index')

const file = new Open.FileAPI.NodeFileSystemFile('file.csv')
const client = new Client('key', 'organization-name', 'dataset-name', 'apiUrl')

client
  .ckanAuthz('http://localhost:5000')
  .then(response => client.push(file, response.result.token))
```

Upload file from **web applications**

```js
import { Client, Open  } from "ckanClient";

const file = new Open.FileAPI.HTML5File(event.target.files[0])
const client = new Client('key', 'organization-name', 'dataset-name', 'api')

const onUploadProgress = progressEvent => {
  let progress = (progressEvent.loaded / progressEvent.total) * 100
  console.log(progress)
}

client
  .ckanAuthz('http://localhost:5000')
  .then(response => client.push(file, response.result.token, onUploadProgress))
```

## Build

This command will create a bundle in `dist`

```
npm run build
```

## Tests

```bash
$ npm test
```

or

```bash
$ yarn test
```

watch the test

```bash
$ npm run test:watch
```

## Changelog

Detailed changes for each release are documented in [CHANGELOG.md](CHANGELOG.md).

## Contributing

Please make sure to read the [CONTRIBUTING.md](CONTRIBUTING.md) Guide before making a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](License) file for details
