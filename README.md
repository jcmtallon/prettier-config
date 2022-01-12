# @jcmtallon/prettier-config
*Playtomic's shared Prettier configuration.*

## Setup

### 1) Install package

```bash
npm install @jcmtallon/prettier-config --save-dev
```

### 2) Install peer dependencies

```bash
npm install prettier@^2.5.1 \
            eslint-config-prettier@^8.3.0, \
            eslint-plugin-prettier@^4.0.0, \
            --save-dev
```

> Install eslint-config plugins only if you are going to setup this config with ESLint (recommended).

if using npm 5+, you can use this shortcut:
```bash
npx install-peerdeps --dev @jcmtallon/prettier-config
```
> If using yarn, you can also use the shortcut described above if you have npm 5+ installed on your machine, as the command will detect that you are using yarn and will act accordingly. 

### 3) Setup with Prettier

Create a `.prettierrc` file and extend `@jcmtallon/prettier-config`.

```js
// .prettierrc.js

module.exports = {
    ...require("@jcmtallon/prettier-config"),
  };
```

### 4) Setup with ESLint

Add `plugin:prettier/recommended` to the extends array in your `.eslintrc.*` file. Make sure to put it last, so it gets the chance to override other configs.

```js
// .eslintrc.*

{
  "extends": [
      "some-other-config-you-use",
      "plugin:prettier/recommended"
    ]
}
```

What does `plugin:prettier/recommended` do?

1. Turns off all ESLint rules that might conflict with Prettier using `eslint-config-prettier`.
2. Set up Prettier as an ESLint rule using `eslint-plugin-prettier`.
3. Adds the following 3 rules to your ESLint rules.

```js 
{
  "rules": {
    "prettier/prettier": "error",
    "arrow-body-style": "off",
    "prefer-arrow-callback": "off"
  }
}
```

And that's it. Now that it is integrated with ESLint, running ESLint will report all code that fails to any Prettier rule. `eslint --fix` or automatic eslint formatting with vscode will also apply any formatting set up in this config.
