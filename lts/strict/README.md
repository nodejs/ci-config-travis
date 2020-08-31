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

The shared configurations only define a list of major versions, which means Travis CI will execute your tests in the _latest_ version of each major release line. If you intend your code to work in earlier versions of that release line, you _should_ explicitly include the earliest version you support in your test matrix, e.g. append the following in your `.travis.yml`:

```
node_js:
  - "10.0.0"
```


### Upgrade timeline

For actual release dates, please check the Node.js [Release Working Group](https://github.com/nodejs/Release/#release-schedule) repository.

This is an example of which versions would be available in each of the files on a certain date:

|                       | `lts/strict/gte-10.yml` | Notes
|-----------------------|-------------------------|-------
| Jul, 2020             | 10, 12                  |
| Nov, 2020             | 10, 12, 14              | In Oct, 2020 v14 reaches LTS and v15 is released
| May, 2021             | 10, 12, 14              | In Apr, 2021 v10 reaches EOL and v16 is released
| Jul, 2021             | 10, 12, 14              | On 1/Jun/2021, v15 reaches EOL
| Nov, 2021             | 10, 12, 14, 16          | In Oct, 2021 V16 reaches LTS and v17 should be released
