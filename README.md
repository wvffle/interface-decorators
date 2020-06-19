# Interface decorators
Interface decorators for JavaScript

## Usage
You'll need babel in your project, see [notes](#JavaScript).

### Example rollup config:
```js
// rollup.config.js
import resolve from '@rollup/plugin-node-resolve'
import commonjs from '@rollup/plugin-commonjs'
import babel from '@rollup/plugin-babel'

export default [{
  input: 'src/index.js',
  output: {
    file: 'public/index.js',
    format: 'esm',
    name: 'core'
  },
  plugins: [
    babel({ 
      sourceMap: true,
      include: ['src/**/*'],
      extensions: ['.js'],
      plugins: [
        '@babel/plugin-proposal-class-properties', 
        ['@babel/plugin-proposal-decorators', { decoratorsBeforeExport: false }]
      ]
    }),
    resolve(),
    commonjs(),
  ]
}]
```

## Example
```js
import { Interface, implement, isImplementing } from 'interface-decorators'

@Interface
class Serializable {
  serialize () {}
  static deserialize () {}
}

@Interface
class Entity {
  distanceTo () {}
}

@implement(Serializable, Entity)
class Player {
  // has to implement serialize, distanceTo and static deserialize
}

const player = new Player()

isImplementing(Player, Entity) // true
isImplementing(player.constructor, Serializable, Entity) // true
```

## Notes

### JavaScript
Well, decorators are not part of the official spec and may never be. By the time of writing this readme they are in [stage-2 proposal](https://github.com/tc39/proposal-decorators)

### TypeScript
I have no idea if they'll work in typescript or not i'm a js dev, not a ts one.
