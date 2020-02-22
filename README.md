### Quick Start
```
git clone --depth 1 https://github.com/milesfrain/purescript-react-basic-hooks-template.git myApp
cd myApp
npm install
npx spago build
npx parcel src/index.html --open
```

### Introduction

This template for [purescript-react-basic-hooks](https://pursuit.purescript.org/packages/purescript-react-basic-hooks/0.4.0) is a direct purescript port of the introductory example of the [official React Hooks documentation](https://reactjs.org/docs/hooks-intro.html).

More examples are available in the [package repository](https://github.com/spicydonuts/purescript-react-basic-hooks).

If you notice any problems with the below setup instructions, or have suggestions on how to make the new-user experience any smoother, please create an issue or pull-request.

Compatible with PureScript compiler 13.6

### Initial Setup

There are two setup options:
* The first option tracks tool versions on a per-project basis, so it is easy to switch between projects that use different compiler versions. A minor inconvenience is that these commands must then be prefixed by `npx` to ensure that the local (not global) versions are run.
* The second option installs tools globally, and this is fine if you plan to keep-up with the latest and greatest compiler version and package sets. Keep in mind that any projects with out-of-date dependencies are at risk of breaking with a compiler upgrade.

You may also use a blend of both approaches, such as tracking local versions of `purescript` and `spago`, but using a global version of `parcel`. A major version bump of `parcel` is unlikely to break your project.

#### Option 1 - Local Toolchain


Install dependencies:
```
npm install
```
Initial compilation:
```
npx spago build
```
Launch webapp:
```
npx parcel src/index.html --open
```

#### Option 2 - Global Toolchain

Install tools globally:
```
npm install -g purescript spago parcel
```
You may then delete these lines listing local development dependencies from `package.json`:
``` json
  "devDependencies": {
    "parcel": "^1.12.4",
    "purescript": "^0.13.6",
    "spago": "^0.14.0"
```
Install remaining react dependencies locally:
```
npm install
```

The remaining commands are the same as "Option 1" but without the `npx` prefix:

Initial compilation:
```
spago build
```
Launch webapp:
```
parcel src/index.html --open
```


### Development Cycle
If you're using an [editor](https://github.com/purescript/documentation/blob/master/ecosystem/Editor-and-tool-support.md#editors) that supports [`purs ide`](https://github.com/purescript/purescript/tree/master/psc-ide) or are running [`pscid`](https://github.com/kRITZCREEK/pscid), you simply need to keep the previous `parcel` command running in a terminal. Any save to a file will trigger an incremental recompilation, rebundle, and web page refresh, so you can immediately see your changes.

If your workflow does not support automatic recompilation, or if you add, remove, or modify module names, then you will need to manually re-run `spago build`.

### Production

When you are ready to create a minified bundle for deployment, run the following command:
```
npx parcel build src/index.html
```

Parcel output appears in the `./dist/` directory. Both development and production builds may be present.
The production output will be much smaller.

``` sh
> ls -hs dist

# Points to either minified or development .js. Depends which command was run most recently.
4.0K index.html

# Production output (minified)
352K src.1da726ad.js
928K src.1da726ad.js.map

# Development output
1.6M src.e31bb0bc.js
2.8M src.e31bb0bc.js.map
```

Deleting this directory before running `parcel build` is a convenient way to ensure there are no irrelevant files.

You can test the production output locally with a tool like [`http-server`](https://github.com/http-party/http-server#installation). It seems that `parcel` should also be able to accomplish this, but it unfortunately will only serve development builds locally.
```
http-server dist -o
```

If everything looks good, you can then upload the contents of `dist` to your preferred static hosting service.