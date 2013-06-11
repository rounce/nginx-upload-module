# nginx-upload-module

This is a fork of the `2.2` branch of the
[nginx-upload-module](https://github.com/vkholodkov/nginx-upload-module) that
allows for:

 * Configurable support for `PUT` and `PATCH` HTTP methods
 * Passing `GET` and `OPTIONS` requests transparently on to the `upload_pass`
   handler

## Versioning

*Current Version*: `2.2.1+veracross.1`

Currently this fork is versioned with a `+veracross` build suffix. This
follows the build metadata portion of
[Semantic Versioning specification](http://semver.org/).

## Documentation

The following documentation covers the features this fork adds. The original
documentation should be used for all other functionality:

 * [English](http://www.grid.net.ru/nginx/upload.en.html)
 * [Russian](http://www.grid.net.ru/nginx/upload.ru.html)

### upload_pass_methods_get_options

This flag (`on`/`off`) configures the upload module to pass `GET` and `OPTIONS`
requests on to the `upload_pass` location without processing them at all.

The nginx-upload-module normally responds to `OPTIONS` requests with a
hard-coded `200 OK` response, which does not allow applications to properly
handle cross-domain `OPTIONS` requests.

With this options turned on, your application code will be invoked for `OPTIONS`
and `GET` requests, allowing for custom responses.

```
location /files {
	upload_pass @my_handler;
	upload_pass_methods_get_options on;
}
```

### upload_allow_methods_put_patch

This flag (`on`/`off`) configures the upload module to allow file upload
handling for the HTTP `PUT` and `PATCH` methods.

The nginx-upload-module normally rejects all requests that do not use `POST`.

```
location /files {
	upload_pass @my_handler;
	upload_allow_methods_put_patch on;
}
```

## Changelog

The [Changelog](Changelog) is maintained with keep a record of all features and
bug fixes.

## Nginx 1.3 and 1.4 Support

Currently neither this version, nor the original nginx-upload-module support
Nginx 1.3.9+. With version 1.3.9 quite a bit of the Nginx internals were
rewritten to support chunked requests.

See https://github.com/vkholodkov/nginx-upload-module/issues/41#issuecomment-15692917
for the original author’s position on Nginx 1.3.9+ compatibility.

## Credits

The nginx-upload-module was written by Valery Kholodkov
(http://www.nginxguts.com/).