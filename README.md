# wbc-version

a hook into npm's version control to create a app.wbc-version.ts.

It will do the following steps:
- bump up the version number (f.e. 'patch' increments 0.0.1 -> 0.0.2)
- start the wbc-version.js script, that will
    - get the new version number
    - get the current branch
    - get the latest commit hash
    - get a new Date() and
    - write them all to the file app.wbc-version.ts in scr/app
- git add scr/app/app.wbc-version.ts
- git push
- git push --tags


src/app/wbc-version.ts file output:
```
export const appVersion = {
  version: '0.0.69',
  branch: '* master',
  commit: 'de8998f',
  date: 'Thu Feb 01 2018 14:48:56 GMT+0100 (CET)'
};
```



## install
Download `wbc-version.js` to root of your project.
In the projects package.json add:
```
  [...]
  "scripts": {
    [...]
    "version": "node ./wbc-version.js && git add ./src/app/app.wbc-version.ts",
    "postversion": "git push && git push --tags"
  },
```



## usage
Code & commit as usual. When ready to release a new version, use
`npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease | from-git]`.


Inside your app, f.e. in app.component.ts you can 
```
import { appVersion } from './app.wbc-version';
console.log(appVersion);
```