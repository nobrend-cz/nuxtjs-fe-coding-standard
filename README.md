# Nuxt.js FE coding standard

Vue CLI plugin that adds FE coding standard to an existing Nuxt project

1. Install Nuxt.js WITHOUT linting
2. Install ESLint

```sh
$ npm i babel-eslint eslint eslint-loader eslint-plugin-vue -D
```

3. Install Stylelint

```sh
$ npm i stylelint stylelint-webpack-plugin -D
```

4. Install FE coding standard

```sh
$ npm i git+https://github.com/nobrend-cz/fe-coding-standard.git -D
```

5. Modify `nuxt.config.js`

```javascript
const StyleLintPlugin = require('stylelint-webpack-plugin');

export default {
  build: {
    extend(config) {

      // ESLint
      config.module.rules.push({
        enforce: 'pre',
        test: /\.(js|vue)$/,
        loader: 'eslint-loader',
        exclude: /(node_modules)/,
        options: {
          fix: true
        }
      })

      // Stylelint
      config.plugins.push(
        new StyleLintPlugin({
          files: [ '{assets,components,layouts,pages}/**/*.{vue,htm,html,css,sss,less,scss,sass}' ],
          fix: true
        })
      )
    }
  }
}
```

6. Add `.eslintrc.js`

```javascript
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true
  },
  parserOptions: {
    parser: 'babel-eslint'
  },
  extends: [
    'plugin:vue/essential',
    './node_modules/fe-coding-standard/eslint-default.json'
  ],
  plugins: ['vue'],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'vue/html-indent': [ 'error', 'tab' ],
  },
}
```

7. Add `.stylelintrc.js`

```javascript
module.exports = {
  extends: [ './node_modules/fe-coding-standard/stylelint-default.json' ],
  rules: {},
};
```

:clap: Done!

Your `devDependencies` in `package.json` should look similar to this now:

```json
{
  "devDependencies": {
    "babel-eslint": "^10.1.0",
    "eslint": "^7.8.1",
    "eslint-loader": "^4.0.2",
    "eslint-plugin-vue": "^6.2.2",
    "fe-coding-standard": "git+https://github.com/nobrend-cz/fe-coding-standard.git",
    "stylelint": "^13.7.0",
    "stylelint-webpack-plugin": "^2.1.0"
  }
}
```
