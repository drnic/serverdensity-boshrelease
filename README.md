# BOSH Release for serverdensity

NOTE: this was an initial spike of a BOSH release to see if Server Density could be supported.

Ultimately, to support all the plugins that come along, each will need to be included in this BOSH release and enabled for a user/server via the deployment manifest.

## Release to your BOSH

To create and upload this release to your BOSH:

```
bosh target BOSH_URL
git clone git@github.com:drnic/serverdensity-boshrelease.git
cd serverdensity-boshrelease
bosh create release
# blobs are automatically downloaded
# name it 'cassandra-dev' or something unique to your bosh
bosh upload release
```

### Finalizing a release

If you create a final release `bosh create release --final`, you must immediately create a new development release. Yeah, this is a bug I guess.

```
[outside vagrant]
bosh create release --final
bosh create release

[inside vagrant as vcap user]
/vagrant/scripts/update examples/default.yml
```


### Alternate configurations

This BOSH release is configurable during deployment with properties. 

Please maintain example scenarios in the `examples/` folder.

To switch between example scenarios, run `sm bosh-solo update examples/FILE.yml` with a different example scenario.

## Uploading to BOSH

Once you have a BOSH release that you like, you can upload it to BOSH and deploy it.

```
bosh upload release
bosh deployment path/to/manifest.yml
bosh deploy
```

Example `properties` for your `manifest.yml` can be taken from the examples in `examples\`

