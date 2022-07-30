# yii2-asset-provider

提供了Yii2应用程序的Bower Asset依赖，以便国内镜像加速。

## 使用阿里云镜像加速composer

[阿里云 Composer 全量镜像](https://mirrors.aliyun.com/composer/)

```json
{
  "repositories": {
    "packagist": {
      "type": "composer",
      "url": "https://mirrors.aliyun.com/composer/"
    }
  }
}
```

然后添加本仓库：`composer require yzchan/yii2-asset-provider ~2.0.45`

不再需要 [composer-asset-plugin](https://github.com/fxpio/composer-asset-plugin) 和 [Asset Packagist](https://asset-packagist.org/)

## 程序配置

```php
return [
    'aliases' => [
        '@bower' => '@vendor/yzchan/yii2-asset-provider/bower-asset',
        '@npm'   => '@bower',
    ],
    // ... other configure
]
```

## yii2-app-advanced(2.0.45) 依赖分析

Yii2高级模版依赖yii2核心库 [yiisoft/yii2](https://github.com/yiisoft/yii2) 和 bootstrap4。

```json
{
  "require": {
    "yiisoft/yii2": "~2.0",
    "npm-asset/bootstrap": "^4.3"
  }
}

```

yii2核心库又依赖如下前端资源：

```json
{
  "require": {
    "bower-asset/jquery": "3.6.*@stable | 3.5.*@stable | 3.4.*@stable | 3.3.*@stable | 3.2.*@stable | 3.1.*@stable | 2.2.*@stable | 2.1.*@stable | 1.11.*@stable | 1.12.*@stable",
    "bower-asset/inputmask": "~3.2.2 | ~3.3.5",
    "bower-asset/punycode": "1.3.*",
    "bower-asset/yii2-pjax": "~2.0.1"
  }
}
```

简单分析可以计算出如下依赖：

```json
{
  "dependencies": {
    "bootstrap": "^4.3",
    "yii2-pjax": "~2.0.1",
    "jquery": ">=1.11.0",
    "inputmask": "~3.3.5",
    "punycode": "~1.3.0"
  }
}
```

通过bower安装，最终安装版本如下：

```text
安装结果
bower jquery#>=1.11.0          install jquery#3.6.0
bower inputmask#~3.3.5         install inputmask#3.3.11
bower bootstrap#^4.3           install bootstrap#4.6.2
bower yii2-pjax#~2.0.1         install yii2-pjax#2.0.7
bower punycode#~1.3.0          install punycode#1.3.2

jquery#3.6.0 vendor/bower-asset/jquery

inputmask#3.3.11 vendor/bower-asset/inputmask
└── jquery#3.6.0

bootstrap#4.6.2 vendor/bower-asset/bootstrap

yii2-pjax#2.0.7 vendor/bower-asset/yii2-pjax
└── jquery#3.6.0

punycode#1.3.2 vendor/bower-asset/punycode

```