# StarUML v3.0.0 + Full Version
a method to get the full version of StarUML

> Note: This is the guide for v3.0+

# Requirements
1. Download & Install StarUML: [https://staruml.io](https://staruml.io/download)
2. Download & Install Node.js: [node.js](https://nodejs.org/en/download)
3. Code editor: notepad, notepad++, sublime, vscode ,etc.

# Step-by-step Instructions
1. Open CMD as Administrator
2. cd C:\Program Files\StarUML\resources
3. Execute
```
npm install -g asar
```
4. Decompile app.asar file
```
asar extract app.asar app
```
5. an app folder and file is going to be created in resources folder
6. Open the app\src\engine\license-manager.js file, comment out the original one, and add a some modifications code below
```
checkLicenseValidity () {
    this.validate().then(() => {
      setStatus(this, true)
    }, () => {
      //setStatus(this, false)
     // UnregisteredDialog.showDialog()
     setStatus(this, true)//这个
    })
  }

  /**
   * Check the license key in server and store it as license.key file in local
   *
   * @param {string} licenseKey
   */
  register (licenseKey) {
    return new Promise((resolve, reject) => {
      $.post(app.config.validation_url, {licenseKey: licenseKey})
        .done(data => {
          var file = path.join(app.getUserPath(), '/license.key')
          fs.writeFileSync(file, JSON.stringify(data, 2))
          licenseInfo = data
          setStatus(this, true)
          resolve(data)
        })
        .fail(err => {
          setStatus(this, true)//这个
          //if (err.status === 499) { /* License key not exists */
           // reject('invalid')
          //} else {
          //  reject()
          //}
        })
    })
  }
```
7. Go back to CMD again, then repackage and replace the original app.asar with this command
```
asar pack app app.asar
```
8. Enjoy.
