# HTMLScriptElement.supports(type) method : Security and Privacy self-review

Author: horo@chromium.org - Last Updated: 2021-09-02

This document is written for a TAG review of [HTMLScriptElement.supports(type) method proposal](script_element_supports.md).
Questions are copied from https://www.w3.org/TR/security-privacy-questionnaire/ . 

## Questions to Consider


1.  What information might this feature expose to Web sites or other parties, and for what purposes is that exposure necessary?

    This feature exposes the information of the availability of new features which use the script element.

1.  Do features in your specification expose the minimum amount of information necessary to enable their intended uses?

    Yes

1.  How do the features in your specification deal with personal information, personally-identifiable information (PII), or information derived from them?

    Thie feature does not deal with personal information.

1.  How do the features in your specification deal with sensitive information?
 
    Thie feature does not deal with sensitive information.

1.  Do the features in your specification introduce new state for an origin that persists across browsing sessions?

    No.

1.  Do the features in your specification expose information about the underlying platform to origins?

    No.

1.  Does this specification allow an origin to send data to the underlying platform?

    No.

1.  Do features in this specification allow an origin access to sensors on a user’s device

    No.

1.  What data do the features in this specification expose to an origin? Please also document what data is identical to data exposed by other features, in the same or different contexts.

    No data is expesed to another origin.
 
1.  Does this specification enable new script execution/loading mechanisms?

    No.

1.  Do features in this specification allow an origin to access other devices?

    No.

1.  Do features in this specification allow an origin some measure of control over a user agent’s native UI?

    No.

1.  What temporary identifiers do the feautures in this specification create or expose to the web?

    None.

1.  How does this specification distinguish between behavior in first-party and third-party contexts?

    It does not distinguish between first-party and third-party contexts.

1.  How do the features in this specification work in the context of a browser’s Private Browsing or Incognito mode?

    Behaviour is identical. No fingerprinting vectors are added.

1.  Does this specification have a "Security Considerations" and "Privacy Considerations" section?

    Yes.

1.  Does this specification allow downgrading default security characteristics?

    No.

1.  What should this questionnaire have asked?

    N/A
