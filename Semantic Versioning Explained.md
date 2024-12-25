Semantic Versioning Explained
Semantic versioning is very easy to explain and leaves very little to interpretation. We have three numbers called major, minor, and patch. If we increment minor, patch is reset to zero (or one). Similarly, if major is incremented, both the minor and the patch are set to zero (or one). Which number is incremented depends on the type of the change we’re releasing.

Given a version number MAJOR.MINOR.PATCH, increment each of the segments using the rules that follow.

PATCH is incremented when we release bug fixes.
MINOR is incremented when new functionality is added in a backward-compatible manner.
MAJOR is incremented when changes are not backward compatible.

If, for example, our application has an API, incrementing the major version would be a clear signal to our users that they would need to adapt or continue using the previous (older) major version (assuming we keep both, as we should). A change in the minor version would mean that users do not need to adapt, even though there are new features included in the release. All other cases would increment only the patch version. 
