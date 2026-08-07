# node-addon-api dependencies

|project|license [^_l]|description [dependencies]|version|source|diff [^_d]|
|-------|-------------|--------------------------|-------|------|----------|
|<a id='node-addon-api' />[node-addon-api](https://github.com/nodejs/node-addon-api)|[MIT](https://github.com/nodejs/node-addon-api/blob/v8.5.0/LICENSE.md 'MIT License')|Module for using N-API from C++ [deps: _nodexp_]| |[upstream](https://github.com/nodejs/node-addon-api 'github.com/nodejs/node-addon-api')|  [intro]|
|<a id='nodexp' />[nodexp](https://nodejs.org/en/blog/release/v22.19.0/)|[MIT](https://raw.githubusercontent.com/nodejs/node/v22.19.0/LICENSE 'MIT License')|node/npm development platform and runtime executable bundled as externpro devel package to build addons|[xpv22.19.0.4](https://github.com/externpro/nodexp/releases/tag/xpv22.19.0.4 'release')|[repo](https://github.com/externpro/nodexp 'github.com/externpro/nodexp')|[diff](https://github.com/externpro/nodexp/compare/v0...xpv22.19.0.4 'github.com/externpro/nodexp/compare/v0...xpv22.19.0.4') [bin]|

![deps](xprodeps.svg 'dependencies')

Dependency version check: all 1 parent-manifest versions match pinned versions.

|diff  |description|
|------|-----------|
|patch |diff modifies/patches existing cmake|
|intro |diff introduces cmake|
|auto  |diff adds cmake to replace autotools/configure/make|
|native|diff adds cmake but uses existing build system|
|bin   |diff adds cmake to repackage binaries built elsewhere|
|fetch |diff adds cmake and utilizes FetchContent|

[^_l]: see [SPDX License List](https://spdx.org/licenses/ '') for a list of commonly found licenses
[^_d]: see table above with description of diff
