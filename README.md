# centralized-multidrive [![stability][0]][1]
[![npm version][2]][3] [![build status][4]][5]
[![downloads][8]][9] [![js-standard-style][10]][11]

Manage multiple hyperdrives in a central location. Stores all `hyperdrive`
databases under `~/.level`.

## Usage
```js
const multidrive = require('centralized-multidrive')
const discovery = require('hyperdiscovery')

const drives = multidrive('my-cool-archive', function (err) {
  if (err) console.error(err)
})

drives.create('cute-cats', (err, drive) => {
  if (err) return console.error(err)

  // drive === [HyperDrive]
  drives.list((err, drives) => {
    if (err) console.error(err)

    // drives === { 'cute-cats': [HyperDrive] }
    Object.keys(drives).forEach((key) => {
      const drive = drives[key]
      const archive = drive.createArchive()
      discovery(archive)
    })
  })
})
```

## API
### drives = centralized-multidrive(name, callback)
Create a new `centralized-multidrive` instance

### drives.list(callback(err, drives))
List all drives in the `centralized-multidrive`. `drives` is a key-value object where keys
are names, and values are hyperdrive instances

### drives.create(name, callback(err, drive))
Create a new named `hyperdrive`

### drives.delete(name, callback(err))
Delete a named `hyperdrive`

## Installation
```sh
$ npm install centralized-multidrive
```

## See Also
- https://github.com/karissa/hyperdrive-archive-swarm
- https://github.com/mafintosh/hyperdrive

## License
[MIT](https://tldrlegal.com/license/mit-license)

[0]: https://img.shields.io/badge/stability-experimental-orange.svg?style=flat-square
[1]: https://nodejs.org/api/documentation.html#documentation_stability_index
[2]: https://img.shields.io/npm/v/centralized-multidrive.svg?style=flat-square
[3]: https://npmjs.org/package/centralized-multidrive
[4]: https://img.shields.io/travis/yoshuawuyts/centralized-multidrive/master.svg?style=flat-square
[5]: https://travis-ci.org/yoshuawuyts/centralized-multidrive
[6]: https://img.shields.io/codecov/c/github/yoshuawuyts/centralized-multidrive/master.svg?style=flat-square
[7]: https://codecov.io/github/yoshuawuyts/centralized-multidrive
[8]: http://img.shields.io/npm/dm/centralized-multidrive.svg?style=flat-square
[9]: https://npmjs.org/package/centralized-multidrive
[10]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square
[11]: https://github.com/feross/standard
