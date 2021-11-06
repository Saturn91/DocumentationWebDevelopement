# Eslint setupt

[source](https://eslint.org/docs/user-guide/getting-started)

- [Javascript](#JS)
- [Typescript](#TS)
- [Issue solving](#issues)

# <a name="JS"> Javascript
## Install (for js)
```
npm install eslint --save-dev
```
## setup config  (package.json should already be available!)
```
npx eslint --init
```
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

## Default configuration

Your .eslintrc.{js,yml,json} configuration file will also include the line:

```
{
    "extends": "eslint:recommended"
}
```
    
Because of this line, all of the rules marked "✓" on the rules page will be turned on. Alternatively, you can use configurations that others have created by searching for "eslint-config" on [npmjs.com](npmjs.com). ESLint will not lint your code unless you extend from a shared configuration or explicitly turn rules on in your configuration.

# <a name="TS"></a>Typescript
## Install 
```
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```
## setup config  (package.json should already be available!)
```
npx touch .eslintrc.json
```

Insert this default config into the file
```
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
} 
```

# <a name='issues'></a> Issue solving

## Error: "Failed to load th TSLint Library..."
Install tslint again in repo and reopen, happened in VS Code

## Error: Not using the local TSLint version...
"Not using the local TSLint version found for 'c:/Users/manue/Documents/GitHub/CAS_FE_Project2_learnWithIndexCards/LearnWithIndexCards/src/app/app.component.ts'
To enable code execution from the current workspace you must enable workspace library execution.tslint(1)"

As decribed on [stackoverflow](https://stackoverflow.com/questions/65228384/tslint-extension-throwing-errors-in-my-angular-application-running-in-visual-stu) you have to do the following steps:

1. In VS Code hit Ctrl + shift + P
2. Enter TSLint: Manage workspace library execution" in the popup + Enter
3. Select submenu "enable workspace library execution" and hit Enter

You should at least have a different Error (or it might work...)

# Error: Cannot read tslint configuration...
"Cannot read tslint configuration - 'Failed to load c:\Users\manue\Documents\GitHub\CAS_FE_Project2_learnWithIndexCards\LearnWithIndexCards\tslint.json: Could not find custom rule directory: node_modules/codelyzer'tslint(1)"

You might have missed the step:
```
npx eslint --init
```
