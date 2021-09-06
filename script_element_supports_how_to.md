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

