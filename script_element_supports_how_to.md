# How to use HTMLScriptElement.supports(type) method

HTMLScriptElement.supports(type) method is currently available in Chrome
(>=95.0.4635.1) behind a flag.

1) Download Chrome Canary
([Android](https://play.google.com/store/apps/details?id=com.chrome.canary),
[Desktop](https://www.google.com/chrome/canary/)).
2) Navigate to `chrome://flags` and enable `Experimental Web Platform features`.
Or add `--enable-blink-features=ScriptElementSupports` command-line switch.
3) Navigate to a test page, e.g. https://horo-t.github.io/explainers/script_element_supports_sample.html


Here is an example of how to use the API:

```javascript
(() => {
  if (!('supports' in HTMLScriptElement)) {
    console.log('Your browser doesn\'t support HTMLScriptElement.supports() method.');
    return;
  }
  console.log('Your browser supports HTMLScriptElement.supports() method.');

  const list = [
    'classic',
    'module',
    'importmap'];
  for (let type of list) {
    if (HTMLScriptElement.supports(type)) {
      console.log('Your browser supports "' + type + '" type.');
    } else {
      console.log('Your browser doesn\'t support "' + type + '" type.');
    }
  }
})();
```

You should see something along the lines of:

```
Your browser supports HTMLScriptElement.supports() method.
Your browser supports "classic" type.
Your browser supports "module" type.
Your browser supports "importmap" type.
```

# What can we do for unsupported browsers?

## Detecting modules support

We can detect the support for modules by checking the existance of `noMoudles`
attribute:

```javascript
function checkModuleSupport() {
  if ('supports' in HTMLScriptElement) {
    return HTMLScriptElement.supports('module');
  }
  return 'noModule' in document.createElement('script');
}
```

Or, we can directly use the `nomodule` attribute of a script elements to load
a clasic script file:

```html
<script type="module" src="app.mjs"></script>
<script nomodule defer src="classic-app-bundle.js"></script>
```

## Detecting importmap support

Without this HTMLScriptElement.supports(type) method, there is no way to check
importmap support synchronously. If we want to check for importmap support in
such browsers, we have to use the asynchronous method, as in the following
example:

```javascript
async function checkImportmapSupport() {
  if ('supports' in HTMLScriptElement) {
    return HTMLScriptElement.supports('importmap');
  }
  const iframe = document.createElement('iframe');
  iframe.style = 'position:absolute;width:0;height:0;border:0;';
  document.body.appendChild(iframe);

  const ng_script =
      'data:text/javascript;base64,' +
      window.btoa('window.IMPORTMAP_CHECK_RESOLVE(false);');
  const ok_script =
      'data:text/javascript;base64,' +
      window.btoa('window.IMPORTMAP_CHECK_RESOLVE(true);');
  const importmap = document.createElement('script');
  importmap.type = 'importmap';
  importmap.textContent =
      '{"imports": {"' + ng_script + '": "' + ok_script + '"}}';
  iframe.contentDocument.body.appendChild(importmap);
  const script = document.createElement('script');
  script.textContent = 'import("' + ng_script + '")';
  const promise = new Promise(resolve => {
    iframe.contentWindow.IMPORTMAP_CHECK_RESOLVE = resolve;
  });
  iframe.contentDocument.body.appendChild(script);
  const result = await promise;
  iframe.remove();
  return result;
}
```
