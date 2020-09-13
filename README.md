Performance checklist for VSF (Vue Storefront) projects.
========================================================

This is checklist extends the official VSF [production guide](https://docs.vuestorefront.io/guide/installation/production-setup.html)
with emphasis on performance.

## Frontend options

- Enable cache for SSR output in Redis. 
Related [json option](https://github.com/DivanteLtd/vue-storefront/blob/master/config/default.json#L13)

```json
"useOutputCacheTagging": true,
"useOutputCache": true,
```

```json
"redis": {
    "host": "localhost",
    "port": 6379,
    "db": 0
},
```
- Setup the Varnish cache over SSR output in Redis
[Varnish module](https://github.com/new-fantastic/vsf-cache-varnish)

This is options allowes only clear any entities by cache tags in Varnish. And includes predefined for VSF [VCL config](https://github.com/new-fantastic/vsf-cache-varnish/blob/master/docker/varnish/config.vcl)

```json
"varnish": {
  "enabled": true,
  "host": "localhost",
  "port": 80
}
```



## Api options

- Setup the Varnish cache for the api requests. Related [VCL config](https://github.com/DivanteLtd/vue-storefront-api/blob/master/docker/varnish/config.vcl)

- Enable cache for resized images processing `"active": true`.
Related [json option](https://github.com/DivanteLtd/vue-storefront-api/blob/master/config/default.json#L333)

```json
"imageable": {
    "caching": {
      "active": true,
      "type": "file",
      "file": {
        "path": "/tmp/vue-storefront-api"
      },
      "google-cloud-storage": {
        "libraryOptions": {},
        "bucket": "",
        "prefix": "vue-storefront-api/image-cache"
      }
    }
  },
```
Have two options to cache resized images on file-system or in Google Cloud.
