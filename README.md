# New React Repo Flow

Since React version keeps getting updates, I can't simply create a repo with my desirable config; the maintainence for syncing might be too high.

## Workflow

When creating a new React repo, follow this list **in the exact order** to get the ideal config:

### Create & Eject


- Create the React repo:

```bash
npx create-react-app my-app-name
```

- *[Optional, but recommended]* Once it's done, **eject**.

```bash
cd my-app-name && yarn eject
```

### ESLint 

- Initiate ESLint:

```bash
eslint --init
```

*During the process, ESLint will ask you about the environment. Remember to select both the browser and node, otherwise variables like `process` and `module` will be treated as undefined by ESLint.*

- Once the ESLint initiation is complete, add this rule:
```json
"rules": {
  "no-unused-vars": "warn"
}
```

- Configure the React plugin for ESLint according to [the official doc](https://github.com/yannickcr/eslint-plugin-react). Add this rule to `.eslintrc.json` to avoid a warning caused by eslint-plugin-react:

```json
  "settings": {
    "react": {
      "version": "detect"
    }
  }
```

- Configure React Hook rules according to [the official doc](https://www.npmjs.com/package/eslint-plugin-react-hooks). Depending on the version, this may not be needed anymore.

- If needed, we can also enable absolute imports for local files according to [this article](https://dev.to/oliverandrich/absolute-imports-with-create-react-app-and-vscode-ihn). Here is the gist:

1. Create `jsconfig.json` in root:
```json
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

2. Modify `.eslintrc`:
```json
{
  "extends": ["react-app", "plugin:import/errors", "plugin:import/warnings"],
  "settings": {
    "import/resolver": {
      "node": {
        "moduleDirectory": ["node_modules", "src/"]
      }
    }
  }
}
```

3. To make Webpack able to load those absolute imports, add this to `.env` at project root:
```
NODE_PATH=src
```

4. Optionally, if that line is the only line in `.env`, we might as well include that in our repository by removing it from `.gitignore`.

### Prettier

- Install Prettier and its configurations:

```bash
yarn add --dev prettier eslint-config-prettier eslint-plugin-prettier
```

Then, in `.eslintrc`, add this config:

```json
{
  "extends": ["plugin:prettier/recommended"]
}
```

If there are multiple entries in `extends`, add the prettier one at the last.

- Add Prettier config by adding this in `.prettierrc`:

```bash
{
  "printWidth": 120,
  "singleQuote": true
}
```

Add these entries to `.prettierignore`:

```
config/
scripts/
```
