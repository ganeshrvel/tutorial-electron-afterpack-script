# Electron Builder AfterPack configuration

- Author: [Ganesh Rathinavel](https://www.linkedin.com/in/ganeshrvel "Ganesh Rathinavel")
- License: [MIT](https://github.com/ganeshrvel/tutorial-electron-afterpack-script/blob/master/LICENSE "MIT")
- Website URL: [https://github.com/ganeshrvel/tutorial-electron-afterpack-script](https://github.com/ganeshrvel/tutorial-electron-afterpack-script/ "https://github.com/ganeshrvel/tutorial-electron-afterpack-script")
- Repo URL: [https://github.com/ganeshrvel/tutorial-electron-afterpack-script](https://github.com/ganeshrvel/tutorial-electron-afterpack-script/ "https://github.com/ganeshrvel/tutorial-electron-afterpack-script")
- Contacts: ganeshrvel@outlook.com


### Introduction

##### There isn't much information available on Electron Builder AfterPack configuration. I have created a sample code which cleans the junk locale directories from the packaged electron app.
##### I have spent a significant amount of time researching how to get this done. This was originally implemented inside [OpenMTP - Advanced Android File Transfer Application for macOS](https://github.com/ganeshrvel/openmtp "OpenMTP - Advanced Android File Transfer Application for macOS").

### Implementation

- Add the below lines inside your *package.json* file

```json
"build": {
    "afterPack": "./internals/scripts/AfterPack.js"
}
```

- Create a file *./internals/scripts/AfterPack.js* and add the below code

```javascript
'use strict';

const path = require('path');
const glob = require('glob');
const fs = require('fs-extra');

exports.default = context => {
  const lprojRegEx = /(en)\.lproj/g;
  const APP_NAME = context.packager.appInfo.productFilename;
  const APP_OUT_DIR = context.appOutDir;
  const PLATFORM = context.packager.platform.name;

  const cwd = path.join(`${APP_OUT_DIR}`, `${APP_NAME}.app/Contents/Resources`);
  const lproj = glob.sync('*.lproj', { cwd });
  const _promises = [];

  switch (PLATFORM) {
    case 'mac':
      lproj.forEach(dir => {
        if (!lprojRegEx.test(dir)) {
          _promises.push(fs.remove(path.join(cwd, dir)));
        }
      });

      break;
    default:
      break;
  }

  return Promise.all(_promises);
};
```


### Contribute
- Fork the repo and create your branch from master.
- Ensure that the changes pass linting.
- Update the documentation if needed.
- Make sure your code lints.
- Issue a pull request!

When you submit code changes, your submissions are understood to be under the same [MIT License](https://github.com/ganeshrvel/tutorial-electron-afterpack-script/blob/master/LICENSE "MIT License") that covers the project. Feel free to contact the maintainers if that's a concern.


### Buy me a coffee
Help me keep the app FREE and open for all.
Paypal me: [paypal.me/ganeshrvel](https://paypal.me/ganeshrvel "paypal.me/ganeshrvel")

### Contacts
Please feel free to contact me at ganeshrvel@outlook.com

### More repos
- [Electron React Redux Advanced Boilerplate](https://github.com/ganeshrvel/electron-react-redux-advanced-boilerplate "Electron React Redux Advanced Boilerplate")
- [OpenMTP  - Advanced Android File Transfer Application for macOS](https://github.com/ganeshrvel/openmtp "OpenMTP  - Advanced Android File Transfer Application for macOS")
- [electron-root-path](https://github.com/ganeshrvel/npm-electron-root-path "Get the root path of an Electron Application")

### License
tutorial-electron-afterpack-script is released under [MIT License](https://github.com/ganeshrvel/tutorial-electron-afterpack-script/blob/master/LICENSE "MIT License").

Copyright © 2018 - 2019 Ganesh Rathinavel
