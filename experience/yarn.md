# Yarn

Yarn is package manager for JavaScript projects, but it solves some problems that the native npm exists.

## Characteristic

### Consistent Depedency Version

Yarn uses `yarn.lock` to lock the versions of the dependencies of packages.
The reason of this is because `package.json` using by npm may using different version of dependencies,
but Yarn always refers the version locked in `yarn.lock`.

### Parallel Installation

The main reason convincing me to use Yarn instead of npm is this one.
(As I think `package-lock.json` should locked the versions, too)
Npm installs the packages sequentially, but Yarn installs in parallel.
This greatly reduces the time used for installing packages.

### Compatibility
Yarn depends on npm, except extra `yarn.lock` is added.
The use of `package.json` is not affected, so it's available for switching from Yarn to npm.

## Commands

Here only lists commands that are mostly used.


List commands
```
yarn help
```

Init New Project
```
yarn init
```

Install dependencies listed in `package.json`
```
yarn install
```
normally, this command updates `yarn.lock`.

with `--frozen-lockfile` flag, does not updates `yarn.lock` and ensures the version in different environment are same.
Error will throw if the version between `package.json` and `yarn.lock` are not compatible.

with `--offline` flag, the installation does not use online resource (local cache instead), so it's even faster and only valid if the packages exist before and the command is run before.


Add dependencies...
```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

... for different environments
```
yarn add [package] --prod # prod dependencies, default
yarn add [package] --dev  # dev dependencies
yarn add [package] --peer # peer dependencies
```

Upgrade dependencies
```
yarn up [package]
yarn up [package]@[version]
yarn up [package]@[tag]
```

Remove dependencies
```
yarn remove [package]
```

Upgrade Yarn
```
yarn set version latest
```

