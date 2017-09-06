# file-driven-development
Utilities for a stateless, serverless development environment.

## Operating System:
- Mac OS currently.

## Goals
- Open resources in the browser.
  - Remove the need to manage development/build servers.
  - Refocus existing resources when they are already open.
- Develop local web applications without needing to host a server, while still being able to make `XMLHTTPRequest`s to your local file system. Normally Chrome will block this ability by default because they believe it poses a security risk to have it enabled by default.
  - `file-driven-development` has a script `localOpen.sh` which opens up a dedicated Chrome instance with this restriction disabled, and therefore allows you to load local `.html` files, which can make requests back to the file system. This is intentionally a dedicated Chrome instance - for local, file system driven development, apart from your other normal Chrome browsing instance, because you don't want to disable this `XMLHTTPRequest` for general browsing.

##### Usage:

```sh
npm install --save-dev git://github.com/jordwalke/file-driven-development.git
osascript path/to/openLocal.osa reuseSearchPattern openFileUrl useCanary
```


- `path/to/openLocal.osa` Path to where `openLocal.osa` was installed
  (typically in `node_modules`).
- `reuseSearchPattern` is the pattern used to search for existing tabs in the dedicated Chrome instance in order to reuse them.
- `openFileUrl` is the file url that you wish to open if it cannot reuse the existing tab (discovered by `reuseSearchPattern`).
- `useCanary` whether or not to use Chrome Canary.


Typicaly, you would run a command like:

```sh
osascript ./node_modules/file-driven-development/scripts/openLocal.osa /myPath/foo.html file:///myPath/foo.html
```

The search string is intentionally not the same as the file path that is opened, because you may want to be a little more loose with the matching to an existing tab. 

##### Caution:

Be aware of the implications of browsing the internet with the relaxed `XMLHTTPRequest` for local file system access. Only use the dedicated Chrome instance that opens for local file system development, and don't later use that running Chrome instance to browse the general internet. You are responsible for safe browsing, so make sure you understand what the scripts in `file-driven-development` are doing.


##### Credit:

Original Script inspired by Rob Mayoff's
[https://gist.github.com/mayoff/1138816](script), but it may likely diverge
significantly over time.
