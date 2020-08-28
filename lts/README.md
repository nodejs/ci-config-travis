# Travis CI imports - Node.js upgrade policy: `lts`

Import configurations from this folder into your `.travis.yml` to automatically start testing in new versions of Node.js as they get released. Long Term Support (LTS) versions will never get removed from these configurations. Non-LTS versions will get removed when they reach End-of-Life and are no longer support.

Please mind that when you remove the supported Node.js versions in _your library_, according to [semver](https://semver.org/), you should be publishing a new major release. This particular upgrade policy is designed for libraries that support _only LTS_ releases, even though non-LTS releases may appear in their test matrix, i.e. a removal of non-LTS release does not imply a semver breaking change if that non-LTS release was not officially support.

Other upgrade policies:

- [`all`](../all) - new major releases get added as they are released, they never get removed
- [`lts/strict`](../lts/strict) - new major releases get added as they reach LTS status, they never get removed   


## Usage example

In your `.travis.yml`, replace the `node_js` section with the following:

```
import:
  - nodejs/ci-config-travis:lts/gte-10.yml
```

- Travis CI will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v10.0.0, will be added to the list as soon as they are released
- Once added, LTS versions will never be removed. Non-LTS versions will be removed when they reach their lifetime.
    - Note that if your policy is to only support LTS versions, then removing the non-LTS version in your test matrix is not a breaking change, as the non-LTS version was never supported (it was only used for test purposes).
