# Please note: This library is a forked version of the main library [arkesel-js](https://github.com/nanadjei/arkesel-js). This is to enable us utilize the kasa platform. I do not own the rights to this library.

# Kasa SMS Javascript Library 

This package enables sending of sms from your javascript application using [Kasa](http://kasa.philangie.com) as a service provider.

## Requirements & Installation

You can install the package via npm:

```bash
npm install kasa-js
```

## Setting API key in .env file

Before you can start sending sms you will need to set your api key and default sender ID in your /.env file
You can find your api key here `http://kasa.philangie.com/user/sms-api/info`
These config files can be changed from the laravel application.

<!-- /.env file -->

KASA_SMS_SENDER_ID=MyApp\
KASA_SMS_API_KEY=YourKeyGoesHere

## Usage Examples

```js
const Kasa from "kasa-js";

const sms = new Kasa("SenderId", "smsApiKey");
```

## Basic sending(uses api_key set in .env file)

```js
// successful response: {"code":"ok","message":"Successfully Send","balance":58995,"user":"Adinkra Pie"}
// error response: {"code":"102","message":"Authentication Failed"}
sms.send('02XXXXXXXXX', 'Your pie will be ready in 5 mins', timestamp = 'In case you want to schedule',
        (callback) => // console.log(callback)
    );
```

## To use a different api key at runtime

```js
sms.withFreshApiKey('API_KEY_GOES_HERE').send('02XXXXXXXX', 'We want to confirm your destination. Adum post office right?', null,
        (callback) => // console.log(callback)
    );
```

## To customise sender Id (must not be more than 11 characters)

```js
sms.from('CompanyName').send('02XXXXXXXX', 'Your pie is ready for dispatch.', null,
        (callback) => // console.log(callback)
    );
```

## Sceduling (sending message at a later time)

```js
// successful response: {"code":"109","message":"Invalid Schedule Time"}
// successful response: {"code":"ok","message":"SMS Scheduled successfully.","balance":58995,"user":"Adinkra Pie"}
const dateTime ='04-05-2020 06:19 PM'; // Must be this format - "d-m-Y h:i A"
sms.schedule(dateTime, '02XXXXXXXX', 'We have arrived at your destination.',
        (callback) => // console.log(callback)
    )
```

## Checking Sms balance

```js
// successful response: {"balance":58995,"user":"Adinkra Pie","country":"Ghana"}
sms.balance((callback) => console.log(callback));
```

## Check balance of a different a kasa account account

```js
sms.withFreshApiKey('API_KEY_GOES_HERE')balance(
        (callback) => // console.log(callback)
    );
```

### Security

If you discover any security related issues, please email nana.elvee@gmail.com instead of using the issue tracker.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
