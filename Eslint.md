# Eslint setupt

[source](https://eslint.org/docs/user-guide/getting-started)

## Steps
1.install
```
npm install eslint --save-dev
```
2. setup configuration file (package.json should already be available!)
```
npx eslint --init
```

## Configuration
There will be a .eslintrc.{js,yml,json} file in your directory after you followed the two installation steps

You will already find some rules specified like this:
```
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```

The names "semi" and "quotes" are the names of rules in ESLint. The first value is the error level of the rule and can be one of these values:
- "off" or 0 - turn the rule off
- "warn" or 1 - turn the rule on as a warning (doesn't affect exit code)
- "error" or 2 - turn the rule on as an error (exit code will be 1)

for the 2nd parameter (i.e. always) checkout [click](https://eslint.org/docs/user-guide/configuring/)

### Default configuration

Your .eslintrc.{js,yml,json} configuration file will also include the line:

```
{
    "extends": "eslint:recommended"
}
```

Because of this line, all of the rules marked "✓" on the rules page will be turned on. Alternatively, you can use configurations that others have created by searching for "eslint-config" on [npmjs.com](npmjs.com). ESLint will not lint your code unless you extend from a shared configuration or explicitly turn rules on in your configuration.
