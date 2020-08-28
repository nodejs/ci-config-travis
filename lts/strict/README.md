# Travis CI imports - Node.js upgrade policy: `lts/strict`

Import configurations from this folder into your `.travis.yml` to automatically start testing in new versions of Node.js as they reach Long Term Support (LTS) status.

Other upgrade policies:

- [`all`](../../all) - new major releases get added as they are released, they never get removed
- [`lts`](../../lts) - new major releases get added as they are released, non-LTS releases get removed when their support lifetime ends, LTS versions never get removed   


## Usage example

In your `.travis.yml`, replace the `node_js` section with the following:

```
import:
  - nodejs/ci-config-travis:lts/strict/gte-10.yml
```

- Travis will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v10.0.0, will be added to the list as soon as they achieve LTS status (i.e. ~6 months after they are first released)
- Once added, versions will never be removed from the list
