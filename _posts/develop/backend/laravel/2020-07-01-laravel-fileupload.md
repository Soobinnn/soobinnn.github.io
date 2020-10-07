---
title: '[Laravel] File Upload'
date: 2020-07-01 08:33:00 -0400
categories: devlog
tags: laravel devlog file upload
---

# File Upload

```
composer require league/flysystem-aws-s3-v3

// 메모리 부족하다고 뜰 시,
COMPOSER_MEMORY_LIMIT=-1 composer require league/flysystem-aws-s3-v3
```

## Setting

S3 드라이브 설정 정보 config/filesystems.php

### Ceph Object 사용 시

config/filesystems.php

```php
...
        's3' => [
            'driver' => 's3',
            'key' => env('AWS_ACCESS_KEY_ID'),
            'secret' => env('AWS_SECRET_ACCESS_KEY'),
            'region' => env('AWS_DEFAULT_REGION'),
            'bucket' => env('AWS_BUCKET'),
            'url' => env('AWS_URL'),
            'endpoint' => env('AWS_URL'),
            'bucket_endpoint' => false,
            'use_path_style_endpoint' => true,
        ],
...
```

참고 [https://github.com/thephpleague/flysystem-aws-s3-v3]
