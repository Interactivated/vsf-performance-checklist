# Performance checklist for VSF (Vue Storefront) projects.

# Frontend options

- Enable cache for SSR output in Redis 
[related config](https://github.com/DivanteLtd/vue-storefront/blob/master/config/default.json#L13)

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
[Varnish module](https://github.com/new-fantastic/vsf-cache-varnish)

This is options allowes only clear any entities by cache tags in Varnish. And includes predefined for VSF [ACL config](https://github.com/new-fantastic/vsf-cache-varnish/blob/master/docker/varnish/config.vcl)

```json
"varnish": {
  "enabled": true,
  "host": "localhost",
  "port": 80
}
```



# Api options

- Enable cache for resized images processing `"active": true`
[related config](https://github.com/DivanteLtd/vue-storefront-api/blob/master/config/default.json#L333)

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
