# Auto-update Node.js version matrix in Travis CI

- This repository is managed by the [Package Maintenance Working Group](https://github.com/nodejs/package-maintenance), see [Governance](https://github.com/nodejs/package-maintenance/blob/master/Governance.md).
- Read more about [Shared Build Configurations in Travis CI](https://docs.travis-ci.com/user/build-config-imports/).

Import configurations from this repository into your `.travis.yml` to automatically start testing in new versions of Node.js as they get released.

## Usage

```
import:
  - nodejs/ci-config-travis:lts/gte-10.yml
  #                          ^       ^
  #                          |       |
  #                          |       ·---------- Miminum version
  #                          ·------------------ Update policy
  # i.e. include all LTS Node.js releases, starting with version 10.x
```

Depending on the support policy of your library/application, you can choose when and which versions get added to your test matrix.

Once added to the list, the LTS versions will never get removed from the list, i.e. you will need to take explicit action to change the minimum version you're importing (note: when you increase the minimum version requirements, you should also bump the major version of your package, to indicate breaking changes according to [semver](https://semver.org/)).

This repository offers three update strategies:

- [`all`](./all) - new major releases get added as they are released, they never get removed
- [`lts`](./lts) - new major releases get added as they are released, non-LTS releases get removed when their support lifetime ends, LTS versions never get removed
- [`lts/strict`](./lts/strict) - new major releases get added as they reach LTS status, they never get removed   


### Examples

#### `lts` policy: use LTS and current Node.js releases, starting with v10.x 

```
import:
  - nodejs/ci-config-travis:lts/gte-10.yml
```

- Travis CI will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v10.0.0, will be added to the list as soon as they are released
- Once added, LTS versions will never be removed. Non-LTS versions will be removed when they reach their lifetime.
    - Note that if your policy is to only support LTS versions, then removing the non-LTS version in your test matrix is not a breaking change, as the non-LTS version was never supported (it was only used for test purposes).


#### `all` policy: use all Node.js releases, starting with v14.x 

```
import:
  - nodejs/ci-config-travis:all/gte-14.yml
```

- Travis will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v14.0.0, will be added to the list as soon as they are released
- Once added, versions will never be removed from the list


#### Strict `lts` policy: use only LTS Node.js releases, starting with v10.x 

```
import:
  - nodejs/ci-config-travis:lts/strict/gte-10.yml
```

- Travis will use the latest version of each release line in the list
- New major Node.js versions, greater or equal to v14.0.0, will be added to the list as soon as they achieve LTS status (i.e. ~6 months after they are released)
- Once added, versions will never be removed from the list
