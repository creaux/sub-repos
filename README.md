# Subrepo

Subrepo is mixture of **git submodules** and **lerna + yarn workspaces monorepo**.

This is due to the fact of ease of interdepenency development. Especially in the situation when one module depends on another and both consume same dependency.

## Development

DO NOT RUN!!! `yarn install` instead start with the following.

`yarn bootstrap`

Will do the trick for interdependency development.

`yarn attach`

WARNING: Depends on `yarn preinstall` which is run automatically.

Makes sure that package based node_modules are linked together also. NOTE: This is more usefull for typings as yarn workspaces installing everything to workspace context.
