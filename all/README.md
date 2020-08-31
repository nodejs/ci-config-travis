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

The shared configurations only define a list of major versions, which means Travis CI will execute your tests in the _latest_ version of each major release line. If you intend your code to work in earlier versions of that release line, you _should_ explicitly include the earliest version you support in your test matrix, e.g. append the following in your `.travis.yml`:

```
node_js:
  - "10.0.0"
```


### Upgrade timeline

For actual release dates, please check the Node.js [Release Working Group](https://github.com/nodejs/Release/#release-schedule) repository.

This is an example of which versions would be available in each of the files on a certain date:

|                       | `all/gte-10.yml`               | Notes
|-----------------------|--------------------------------|-------
| Jul, 2020             | 10, 11, 12, 13, 14             |
| Nov, 2020             | 10, 11, 12, 13, 14, 15         | In Oct, 2020 v14 reaches LTS and v15 is released
| May, 2021             | 10, 11, 12, 13, 14, 15, 16     | In Apr, 2021 v10 reaches EOL and v16 is released
| Jul, 2021             | 10, 11, 12, 13, 14, 15, 16     | On 1/Jun/2021, v15 reaches EOL
| Nov, 2021             | 10, 11, 12, 13, 14, 15, 16, 17 | In Oct, 2021 V16 reaches LTS and v17 should be released
