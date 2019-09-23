# Subrepo

Subrepo is mixture of **git submodules** and **lerna + yarn workspaces monorepo**.

This is due to the fact of ease of interdepenency development. Especially in the situation when one module depends on another and both consume same dependency.

## Development

`yarn bootstrap`

Will do the trick for interdependency development.
