# Library for using websms.com SMS services with yii2 framework

[![Latest Stable Version](https://poser.pugx.org/simialbi/yii2-websms-com/v/stable?format=flat-square)](https://packagist.org/packages/simialbi/yii2-websms-com)
[![Total Downloads](https://poser.pugx.org/simialbi/yii2-websms-com/downloads?format=flat-square)](https://packagist.org/packages/simialbi/yii2-websms-com)
[![License](https://poser.pugx.org/simialbi/yii2-websms-com/license?format=flat-square)](https://packagist.org/packages/simialbi/yii2-websms-com)

## Installation
The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
$ php composer.phar require --prefer-dist simialbi/yii2-websms-com
```

or add

```
"simialbi/yii2-websms-com": "^1.0.0"
```

to the `require` section of your `composer.json`.

## Usage

In order to use this component, you will need to:

1. [Setup component](#setup-component) your application so that the module is available.

### Setup component

```php
return [
    // [...]
    'components' => [
        'sms' => [
            'class' => 'simialbi\yii2\voting\sms\Connection',
            'baseUrl' => 'https://api.websms.com',
            'token' => '<your api token>',
            'sendUrl' => '/rest/smsmessaging/simple'
        ]
    ]
];
```

## Example Usage

To send a message create a new `Message` instance and set at least the content and recipients.

```php
<?php
 /** @var \simialbi\yii2\websms\Connection $sms */
$sms = Yii::$app->get('sms', true);
$message = $sms->createMessage();
$message
    ->id('my-test-id-' . uniqid())
    ->category($message::CATEGORY_INFORMATIONAL)
    ->content("This is a test\nwith multpile lines")
    ->type($message::MESSAGE_TYPE_TEXT)
    ->addRecipient('4367612345678');
$response = $message->send();

if ($response->isOk) {
    echo 'success';
} else {
    echo 'failure';
}
```

## License

**yii2-websms-com** is released under MIT license. See bundled [LICENSE](LICENSE) for details.
