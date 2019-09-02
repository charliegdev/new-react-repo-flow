# New React Repo Flow

Since React version keeps getting updates, I can't simply create a repo with my desirable config; the maintainence for syncing might be too high.

## Flow

When creating a new React repo, follow this list to get the ideal config:

1. Create the React repo:

```bash
npx create-react-app my-app-name
```

1. Once it's done, **eject**.

```bash
cd my-app-name && yarn eject
```

1. Configure ESLint:

```bash
eslint --init
```

During the process, ESLint will ask you about the environment. Remember to select both the browser and node, otherwise variables like `process` and `module` will be treated as undefined by ESLint.

1. Configure the React plugin for ESLint according to [the official doc](https://github.com/yannickcr/eslint-plugin-react).
1. Configure React Hook rules according to [the official doc](https://www.npmjs.com/package/eslint-plugin-react-hooks). Depending on the version, this may not be needed anymore.

1. Install Prettier:

```bash
yarn add --dev prettier
```

1. Configure Prettier with ESLint:

```bash
yarn add --dev eslint-config-prettier eslint-plugin-prettier
```

Then, in `.eslintrc`, add this config:

```json
{
  "extends": ["plugin:prettier/recommended"]
}
```

If there are multiple entries in `extends`, add the prettier one at the last.

1. Add Prettier config by adding this in `.prettierrc`:

```bash
{
  "printWidth": 120,
  "singleQuote": true
}
```

1. Add these entries to `.prettierignore`:

```
config/
scripts/
```
