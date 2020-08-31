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

The shared configurations only define a list of major versions, which means Travis CI will execute your tests in the _latest_ version of each major release line. If you intend your code to work in earlier versions of that release line, you _should_ explicitly include the earliest version you support in your test matrix, e.g. append the following in your `.travis.yml`:

```
node_js:
  - "10.0.0"
```


### Upgrade timeline

For actual release dates, please check the Node.js [Release Working Group](https://github.com/nodejs/Release/#release-schedule) repository.

This is an example of which versions would be available in each of the files on a certain date:

|                       | `lts/gte-10.yml`        | Notes
|-----------------------|-------------------------|-------
| Jul, 2020             | 10, 12, 14              |
| Nov, 2020             | 10, 12, 14, 15          | In Oct, 2020 v14 reaches LTS and v15 is released
| May, 2021             | 10, 12, 14, 15, 16      | In Apr, 2021 v10 reaches EOL and v16 is released
| Jul, 2021             | 10, 12, 14, 16          | On 1/Jun/2021, v15 reaches EOL and ⚠️ is removed from `lts` policy files
| Nov, 2021             | 10, 12, 14, 16, 17      | In Oct, 2021 V16 reaches LTS and v17 should be released
