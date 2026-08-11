# Quick start

{% note info "" %}

If you want to get started with development quickly, use the [quick guide](https://github.com/diplodoc-platform/diplodoc/blob/master/DEVELOPMENT.md) in the root repository.

{% endnote %}

The diplodoc platform is developed based on a set of independent modules located in the GitHub organization [diplodoc-platform](https://github.com/diplodoc-platform).

Each module can be developed either separately or as part of a [metapackage](./metapackage.md).

The easiest way to start developing any module in the system is to launch a preconfigured GitHub Codespace in the corresponding repository.

You can read more about working with GitHub Codespaces in the [official documentation](https://docs.github.com/en/codespaces/getting-started/quickstart).

## Preparing a module

After creating a codespace, wait for the postCreateCommand to complete (~3 min). 

At this stage, several preparatory actions take place:
- installation of NodeJS packages required by the module
- preliminary build of the module (`npm run build`)
- basic code quality checks (`npm run lint`)
- basic tests (`npm run test`)

When the preparation is successfully completed, i.e., the module builds and passes the basic checks, it is ready for [making changes](#add-changes). 

## Preparing the metapackage

Development within a metapackage simplifies making changes to several modules at once.

After creating a codespace, wait for the postCreateCommand to complete (~3 min).

At this stage, several preparatory actions take place:
- linking git submodules
- installation of required NodeJS packages in npm workspaces mode
- preliminary build of the module graph for the CLI project (`npx nx build @diplodoc/cli`)

By default, code quality checks and tests are not run when initializing the metapackage.
You can run them yourself by executing `npm run lint` and `npm run test` in the root directory, respectively.
This will run the corresponding checks in all dependent modules.

When the preparation is successfully completed, i.e., the module builds and passes the basic checks, it is ready for [making changes](#add-changes). 

## Making changes {add-changes}

When making changes, you need to ensure that the code quality checks (`npm run lint` and `npm run test`) in the modified module still pass without errors.

After that, you can proceed to [creating commits and a pull request](./contribution.md).
