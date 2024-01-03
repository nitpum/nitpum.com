---
title: Make lint-staged + eslint work in monorepo
author: nitpum
date: 2024-01-03T22:38:16+07:00
lastmod: 2024-01-03T19:02:49.413Z
tags:
    - eslint
    - lint-staged
    - monorepo
    - lint
toc: false
---

Imagine a monorepo project that structure like this

```bash
.
├── .eslintrc.js
├── .husky
├── .lintstagedrc.json
├── package.json
└── packages
    ├── app
    │   ├── index.js
    │   └── package.json
    └── ui
        ├── index.js
        └── package.json
```

And has eslint command in `.lintstagedrc.json`

```json
{ "*.js": ["eslint --fix"] }
```

In the example, when lint-staged runs when has .js staged files it will invoke `eslint --fix` to fix the file.

Normal behavior of lint-staged is run command in the project root directory and pass absolute file path as argument e.g.

```bash
eslint --fix /home/user/project/package/app/index.js /home/user/project/package/ui/index.js
```

In the most cases, this is not a problem and usually this is a normal config for non-monorepo project.

However, the problem will occur when some packages has its own eslint config

```bash {hl_lines=11}
.
├── .eslintrc.js
├── .husky
├── .lintstagedrc.json
├── package.json
└── packages
    ├── app
    │   ├── index.js
    │   └── package.json
    └── ui
        ├── .eslintrc.js	# <--- specific eslint config for ui
        ├── index.js
        └── package.json
```

When lint-staged runs, it will run `eslint --fix` in the project root directory and eslint will picks the closest config file which is `./.eslintrc.js` even the staged file is in `./packages/ui` (that should uses config from `./packages/ui/.eslintrc.js` instead) which make eslint invalid.

To fix the problem, just add `.lintstagedrc.json` to package that need to run script in package directory in this cases is `./packages/ui/.lintstagedrc.json`

```bash {hl_lines=12}
.
├── .eslintrc.js
├── .husky
├── .lintstagedrc.json
├── package.json
└── packages
    ├── app
    │   ├── index.js
    │   └── package.json
    └── ui
        ├── .eslintrc.js
        ├── .lintstagedrc.json	# <-- Just add this!
        ├── index.js
        └── package.json
```

That's it!

Now when has staged file in `./packages/ui` lint-staged will run separate `eslint --fix` in `./packages/ui`. For the other staged file it still run `eslint --fix` in the project root directory.

lint-staged has [section](https://github.com/lint-staged/lint-staged?tab=readme-ov-file#how-to-use-lint-staged-in-a-multi-package-monorepo) explain about this and how to setup in monorepo that you can read further more.
