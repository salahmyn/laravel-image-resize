# Image Resize Helper for Laravel 5.x
#### Fork from [MaximumAdvertising/laravel-image-resize](https://github.com/MaximumAdvertising/laravel-image-resize)

Dynamically resize an image and returns the URL using Intervention and Storage

[![Latest Stable Version](https://poser.pugx.org/maximumadvertising/laravel-image-resize/v/stable)](https://packagist.org/packages/maximumadvertising/laravel-image-resize)
[![Latest Unstable Version](https://poser.pugx.org/maximumadvertising/laravel-image-resize/v/unstable)](https://packagist.org/packages/maximumadvertising/laravel-image-resize)

## Require

- Laravel 5+
- Intervention Image ^2.4

## Supported Filesystem Drivers

- Local
- S3
- Oss (Aliyun Cloud Storage)

## Installation

This package can be installed through Composer.

```bash
composer require salahmyn/laravel-image-resize
```

For Laravel 5.4 and lower, you'll have to register the service provider and alias manually.

Add to service providers

```php
Mxmm\ImageResize\ImageResizeServiceProvider::class,
 ```

And alias
```php
'ImageResize' => Mxmm\ImageResize\Facade::class,	
```

Publish config and assets (Optional)
```bash
php artisan vendor:publish --provider="Mxmm\ImageResize\ImageResizeServiceProvider"
```

## Usage

Accepted parameters:

```php
/**
 * @param string|null $path
 * @param int|null $width
 * @param int|null $height
 * @param string $action
 * @return string
 */
public static function url(string $path = null, int $width = null, int $height = null, string $action = 'fit' , $disk = null): string
```

In HTML:
```html
<img src="{{ ImageResize::url('originalDir/filename.jpg', width, height, [action]) }}" />
```

Fit (resize & crop) an image to 200x200px 
```html
<img src="{{ ImageResize::url('originalDir/filename.jpg', 200, 200, 'fit') }}" />
```

Resize an image to 200x200px 
```html
<img src="{{ ImageResize::url('originalDir/filename.jpg', 200, 200, 'resize') }}" />
```

Fit (resize & crop) an image to 200px width, with auto height
```html
<img src="{{ ImageResize::url('originalDir/filename.jpg', 200, null, 'fit') }}" />
```

Fit (resize & crop) an image to 200px width, with auto height
```html
<img src="{{ ImageResize::url('originalDir/filename.jpg', 200, null, 'fit') }}" />
```

sample output
```html
<img src="https://localhost/thumbs/originalDir/fit/200x200/filename.jpg" />
```

### alias [asset]
an `assets` drive in config `filesystems` is required to use `asset` method which handle files in `public` directory

```php
<?php

return [

    /*
    |-----------------------------------------------
    | Default Filesystem Disk
    |-----------------------------------------------
    |
    */
    // ...
    
    'disks' => [
        // ...

        'assets' => [
            'driver' => 'local',
            'root' => public_path('assets'),
        ],
    ];

```

In HTML:
```html
<img src="{{ ImageResize::asset('originalDir/filename.jpg', width, height, [action]) }}" />
```

## Tests

Run tests with:

```bash
vendor/bin/phpunit
```