# Subrepo

Subrepo is mixture of **git submodules** thus **npm separated modukes** and **yarn workspaces**.

Developer can thus develop package in **Mono-repo Mode** or **Single-repo Mode**. **Mono-repo Mode** means that we will checkout subrepo package and then all opeartions are done using **yarn** with help of **yarn workspaces**. **Single-repo mode** suppose to checkout individual pakcage using git run all operations using **npm**.

## Development

1. To start just run `yarn`. If you do reinstalling and don't want to update hooks run `HUSKY_SKIP_INSTALL=1 yarn`.
2. Then go to desired package.

### Mono-repo mode

As dependencies are installed using yarn only _yarn.lock_ is updated. To make sure that _package-lock.json_ for required package is update too run in package context following command.

`npm i --package-lock-only`

This is usually required when `npm ci --dry-run` files as pre-push hook. Required everytime there is new dependency installed.

## Git Hooks & Husky

Husky doesn't support **single package architecture as part of monorepo**. Means Husky supports only eancapsulating monorepo for running git hooks for child packages.

### Monorepo package _yarn_

To be able to separate its behavior per each package and run different hooks per each package. We are using specific setup here.

| In monorepo mode _.huskyrc_ in the root is used and _.huskyrc_ file per each package is ignored.

Contains all hooks which are triggering **package.json scripts in individual packages**. To achieve that following command is used:

`yarn workspace $PACKAGE husky:pre-commit`

Where package is environmental variable which has to be set like for example `PACKAGE=@pyxismedia/lib-react`.

This assumes that each package has to have script like `"husky:pre-commit": "lint-staged"` for example to run lint operation on commit.

#### Automatic PACKAGE recognition

Update `.git/modules/package/{PACKAGE_DIRNAME}/hooks/{HOOK}` and put before the first line the following.

```
export PACKAGE=@pyxismedia/{PACKAGE_NAME}
```

Where PACKAGE_NAME is dir `packages/{PACKAGE_NAME}` from the subrepo root.

### Single package _npm_

| In Single-Repo Mode _.huskyrc_ in package is used.

Each package contains _.huskyrc_ which has to be in sync with `"husky:{hook-name}": "{script}"` in package.json file to make sure same operation is proceed on build.
