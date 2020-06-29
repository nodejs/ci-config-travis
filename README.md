# Shared Travis Configuration Imports

- This repository is managed by the [package-maintenance team](https://github.com/nodejs/package-maintenance).
- Read more about [Shared Build Configurations in Travis CI](https://docs.travis-ci.com/user/build-config-imports/).

## Usage

Replace the list of `node_js` versions in your `.travis.yml` with one of the available files.

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
