# Auto-updated Node.js version matrix in Travis CI

- This repository is managed by the [Package Maintenance Working Group](https://github.com/nodejs/package-maintenance), see [Governance](https://github.com/nodejs/package-maintenance/blob/master/Governance.md).
- Read more about [Shared Build Configurations in Travis CI](https://docs.travis-ci.com/user/build-config-imports/).

Import configurations from this repository into your `.travis.yml` to automatically start testing in new versions of Node.js as they get released.

## Usage

In your `.travis.yml`, replace the `node_js` section with the following:

```
import:
  - nodejs/ci-config-travis:lts/gte-10.yml
  #                          ^       ^
  #                          |       |
  #                          |       ·---------- Miminum version
  #                          ·------------------ Upgrade policy
  # i.e. include all LTS Node.js releases, starting with version 10.x
```

Depending on the support policy of your library/application, you can choose when and which versions get added to your test matrix.

Once added to the list, the Long Term Support (LTS) versions will never get removed from the list, i.e. you will need to take explicit action to change the minimum version you're importing (note: when you increase the minimum version requirements, you should also bump the major version of your package, to indicate breaking changes according to [semver](https://semver.org/)).

This repository offers three upgrade policies:

- **[`all`](./all)** - new major releases get added as they are released, they never get removed
- **[`lts`](./lts)** - new major releases get added as they are released, non-LTS releases get removed when their support lifetime ends, LTS versions never get removed
- **[`lts/strict`](./lts/strict)** - new major releases get added as they reach LTS status, they never get removed   
