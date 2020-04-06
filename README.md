# XRPackage THREE.js template

## What's included

### `manifest.json`

Specifies the type of package (`webxr-site`) and version, and the entrypoint file (`index.html`).

### `index.html`

The main code for the package.

### Other files

Assets that go along with the package.

## Prerequisites

Get `xrpk`

```bash
npm install -g xrpk
```

## Build

Clone this repo

```bash
git clone https://github.com/webaverse/xrpackage-threejs-template.git
```

Build the template

```bash
cd xrpackage-threejs-template
xrpk build .
```

## Run

### Run XRPackage in a test room

```bash
xrpk run a.wbn
```

You should see a spinning cube. You can enter VR.

### Run the XRPackage programmatically

Instantiate an `XRPackageEngine`, `.add` an `XRPackage` to it, and hook up the DOM.

```js
<script type=module>
import {XRPackageEngine, XRPackage} from 'https://xrpackage.org/xrpackage.js';

(async () => {

const pe = new XRPackageEngine();

const res = await fetch('a.wbn'); // this is the file we built earlier
const arrayBuffer = await res.arrayBuffer()
const packageFile = new Uint8Array(arrayBuffer);
const p = new XRPackage(packageFile);
pe.add(p);

// show the canvas in the document
document.body.add(pre.domElement);

// enter XR when we click the canvas
pre.domElement.addEventListener('click', e => {
  navigator.xr.requestSession('immersive-vr', {
    optionalFeatures: [
      'local-floor',
      'bounded-floor',
    ],
  }).then(session => {
    pe.setSession(session);
  });
});

})();
</script>
```

### Run the XRPackage in MetaRTC

- Should behave like any other package
- Currently need to publish it so it shows up globally

## TODO

- Multiple apps example (just `.add` more packages)
- Programmatically position apps (needs API)