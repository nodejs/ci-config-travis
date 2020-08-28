# Travis CI imports - Node.js upgrade policy: `all`

Import configurations from this folder into your `.travis.yml` to automatically start testing in new versions of Node.js as they get released.

Other upgrade policies:

- [`lts`](../lts) - new major releases get added as they are released, non-LTS releases get removed when their support lifetime ends, LTS versions never get removed
- [`lts/strict`](../lts/strict) - new major releases get added as they reach LTS status, they never get removed   


## Usage example

In your `.travis.yml`, replace the `node_js` section with the following:

```
import:
  - nodejs/ci-config-travis:all/gte-14.yml
```

- Travis will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v14.0.0, will be added to the list as soon as they are released
- Once added, versions will never be removed from the list
