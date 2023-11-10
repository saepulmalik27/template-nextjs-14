## Template Nextjs 14 (typescript, tailwindcss, jest, rtl, eslint, prettier, husky, lint-staged, commitlint, commitizen)

project ini menggunakan [Next.js](https://nextjs.org/) 14 project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) dan tambahan tools yang sering gua pake saat setup project nextjs

## Cara Install

1. jalankan command `npx create-next-app@latest`
2. install _husky_ `npx husky-init && yarn` dan jalankan command `yarn prepare`
3. install _prettier_ ` yarn add -D prettier eslint-config-prettier eslint-plugin-prettier prettier-plugin-tailwindcss`
4. setup file `.eslintrc.json`

```
{
  "extends": ["next/core-web-vitals", "prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier":[ "warn",
    {
      "endOfLine": "auto"
    }]
  }
}
```

5. add .prettierrc.json file `touch .prettierrc.json` di root project, dan tambahkan code dibawah

```
{
  "trailingComma": "es5",
  "semi": true,
  "tabWidth": 2,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "plugins": ["prettier-plugin-tailwindcss"]
}

```

6. install lint-staged `yarn add -D lint-staged`
7. tambahkan script ini di _`package.json`_

```
scripts : {
    ...
    "lint-staged": "lint-staged",
    "type-check": "tsc --project tsconfig.json --pretty --noEmit && echo ",
}
```

8. add file .lintstagedrc.js di root project `touch .lintstagedrc.json` dan tambahkan code dibawah

```
module.exports = {
  // Run type-check on changes to TypeScript files
  '**/*.ts?(x)': () => 'yarn type-check',
  // Lint & Prettify TS and JS files
  '**/*.(ts|tsx|js|mjs)': (filenames) => [
    `yarn lint . ${filenames.join(' ')}`,
    `yarn prettier --write ${filenames.join(' ')}`,
  ],
  // Prettify only Markdown and JSON files
  '**/*.(md|json)': filenames => `yarn prettier --write ${filenames.join(' ')}`
};

```

9. Ganti `yarn test` di file .husky/pre-commit `yarn lint-staged`
10. add commitlint `yarn add -D @commitlint/config-conventional @commitlint/cli` add file commitlint.config.js `touch commitlint.config.js`
11. add commitizen `yarn add -D commitizen` dan tambahkan file .cz.json di root project `touch .cz.json`dan tambahkan code dibawah

```
{
  "path": "cz-conventional-changelog"
}
```

12. add commit-msg `npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'`
13. add post-merge `npx husky add .husky/post-merge 'yarn'`
