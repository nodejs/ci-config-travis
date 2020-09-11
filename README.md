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

### Upgrade timeline

For actual release dates, please check the Node.js [Release Working Group](https://github.com/nodejs/Release/#release-schedule) repository.

This is an example of which versions would be available in each of the files on a certain date:

|                       | `all/gte-10.yml`               | `lts/gte-10.yml`        | `lts/strict/gte-10.yml` | Notes
|-----------------------|--------------------------------|-------------------------|-------------------------|-------
| Jul, 2020             | 10, 11, 12, 13, 14             | 10, 12, 14              | 10, 12                  |
| Nov, 2020             | 10, 11, 12, 13, 14, 15         | 10, 12, 14, 15          | 10, 12, 14              | In Oct, 2020 v14 reaches LTS and v15 is released
| May, 2021             | 10, 11, 12, 13, 14, 15, 16     | 10, 12, 14, 15, 16      | 10, 12, 14              | In Apr, 2021 v10 reaches EOL and v16 is released
| Jul, 2021             | 10, 11, 12, 13, 14, 15, 16     | 10, 12, 14, 16          | 10, 12, 14              | On 1/Jun/2021, v15 reaches EOL and ⚠️ is removed from `lts` policy files (`lts/strict` never has this version included and `all` keeps it)
| Nov, 2021             | 10, 11, 12, 13, 14, 15, 16, 17 | 10, 12, 14, 16, 17      | 10, 12, 14, 16          | In Oct, 2021 V16 reaches LTS and v17 should be released


## Including the minimum supported version

The shared configurations only define a list of major versions, which means Travis CI will execute your tests in the _latest_ version of each major release line. If you intend your code to work in earlier versions of that release line, you _should_ explicitly include the earliest version you support in your test matrix, e.g. append the following in your `.travis.yml`:

```
node_js:
  - "10.0.0"
```

This will ensure that you do not accidentally use features added in v10.1+, as they would be considered breaking changes for the consumers of your library.

Should you chose to only support the latest version of any major release line, there currently is no supported way to define that via the `engines` field in your `package.json`, however you could communicate this using [Document support levels](https://github.com/nodejs/package-maintenance/blob/master/docs/PACKAGE-SUPPORT.md) (i.e. the `support` field or alternative locations).
