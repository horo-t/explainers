# HTMLScriptElement.supports(type) method

Author: horo@chromium.org - Last Updated: 2021-09-01

## Summary

Provides a unified way to detect new features that use script elements.

## Motivation

Currently there is no simple way to know what kind of types can be used for `HTMLScriptElement`’s `type` attribute. 

There are several new feature proposals using the script element.
- [Import maps](https://github.com/WICG/import-maps) use `type="importmap"`.
- [Speculation rules](https://github.com/jeremyroman/alternate-loading-modes/blob/main/triggers.md#speculation-rules) use `type="speculationrules"`.
- [Bundle preloading](https://github.com/WICG/resource-bundles/) use `type="bundlepreload"`.

We can use the `nomodule` attribute to detect the `module` type support as [this example](https://html.spec.whatwg.org/multipage/scripting.html#script-nomodule-example) shows.
But there is no unified method to detect such new features. (E.g.: https://github.com/WICG/import-maps/issues/171)
If we have the `HTMLScriptElement.supports(type)` method which is like `HTMLLinkElement.relList.supports()`, we can easily detect such features.

## Usage

```javascript
const script = document.createElement('script');
if (script.supports('importmap')) {
  console.log('Your browser supports import maps.');
}
if (script.supports('speculationrules')) {
  console.log('Your browser supports speculationrules.');
}
if (script.supports('bundlepreload')) {
  console.log('Your browser supports bundlepreload.');
}
```

## Security Considerations

There are no known security impacts of this API.

## Privacy Considerations

This API can be used for fingerprinting by checking the availability of each feature.
However, the Web Platform Design Principles require that each feature be [detectable](https://w3ctag.github.io/design-principles/#feature-detect).
And this API itself only introduces one bit of information about the availability of the API itself.

## Links

- Spec issue: https://github.com/whatwg/html/issues/6472
- Spec change prototype: https://github.com/whatwg/html/compare/main...horo-t:HTMLScriptElement_supports
- Chrome Platform Status: https://www.chromestatus.com/feature/5712146835963904
- Chromium tracking issue: https://crbug.com/1245528
- Chromium prototype CL: https://chromium-review.googlesource.com/c/chromium/src/+/3133553
- Security and Privacy self-review: [script_element_supports_security_and_privacy_review.md](script_element_supports_security_and_privacy_review.md)
