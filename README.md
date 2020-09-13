# Performance checklist for VSF (Vue Storefront) projects.

# Frontend options

- Enable cache for SSR output in Redis 
[reference to config](https://github.com/DivanteLtd/vue-storefront/blob/master/config/default.json#L13)

```json
"useOutputCacheTagging": false,
"useOutputCache": false,
```

```json
"redis": {
    "host": "localhost",
    "port": 6379,
    "db": 0
  },
```
- Varnish cache over SSR output in Redis


# Api options

- Enable cache for resized images processing `"active": true`
[Api config](https://github.com/DivanteLtd/vue-storefront-api/blob/master/config/default.json#L333)

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
