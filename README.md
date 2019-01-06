# Nginx-Image-Filter

## It's a nginx image resizer to be specify. We use in our Back-end CMS.

## How to load Module
```
Tutorial [here](https://zaiste.net/nginx_image_server_with_image_filter_secure_link_modules/).
```

## Technology used
```
Nginx
Module - ngx_http_image_filter_module
Terminal
```

## Sample Configuration 
```
location /img/ {
    proxy_pass   http://backend;
    image_filter resize 150 100;
    image_filter rotate 90;
    error_page   415 = /empty;
}

location = /empty {
    empty_gif;
}
```

## Directives
```
Syntax:	image_filter **off**;
image_filter **test**;
image_filter **size**;
image_filter **rotate 90 | 180 | 270**;
image_filter **resize width height**;
image_filter **crop width height**;
Default:	
image_filter off;
Context:	location
```

Sets the type of transformation to perform on images:

**off**

turns off module processing in a surrounding location.

**test**

ensures that responses are images in either JPEG, GIF, PNG, or WebP format. Otherwise, the 415 (Unsupported Media Type) error is returned.

**size**

outputs information about images in a JSON format, e.g.:
> { "img" : { "width": 100, "height": 100, "type": "gif" } }

In case of an error, the output is as follows:
> {}

**rotate 90|180|270**

rotates images counter-clockwise by the specified number of degrees. Parameter value can contain variables. This mode can be used either alone or along with the resize and crop transformations.

**resize width height**

proportionally reduces an image to the specified sizes. To reduce by only one dimension, another dimension can be specified as “-”. In case of an error, the server will return code 415 (Unsupported Media Type). Parameter values can contain variables. When used along with the rotate parameter, the rotation happens after reduction.

**crop width height**

proportionally reduces an image to the larger side size and crops extraneous edges by another side. To reduce by only one dimension, another dimension can be specified as “-”. In case of an error, the server will return code 415 (Unsupported Media Type). Parameter values can contain variables. When used along with the rotate parameter, the rotation happens before reduction.

Follow more in [here](http://nginx.org/en/docs/http/ngx_http_image_filter_module.html).



