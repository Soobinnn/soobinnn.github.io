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

S3 드라이브 설정 정보 config/filesystems.php

참고 [https://github.com/thephpleague/flysystem-aws-s3-v3]
