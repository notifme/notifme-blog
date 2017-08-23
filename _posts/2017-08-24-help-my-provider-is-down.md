---
layout: post
title:  "Your (SMS | email) provider is down!? :fire: :fire: :fire:"
date:   2017-08-24 02:00:00 +0100
banner_image: matthew-kane-205770.jpg
author: David Brown
comments: true
---
*By [David Brown](https://twitter.com/BDavid24)*

It might (hopefully) be occasional, but it happens. I've seen providers not responding because:
- They were doing scheduled maintenance
- They blocked the account because:
  - of a spike the day before :scream:
  - credit card was refused and nobody read the reminders :see_no_evil:
- They were simply down

Well, keep calm and use Notif.me!&nbsp; :fire_engine:
<!--more-->

## What is Notif.me?

[Notif.me](https://github.com/notifme/notifme-sdk) is an **open source** Node.js library to send all kinds of transactional notifications. It allows you to use **multiple providers** and a **fallback strategy** out of the box.

<p align="center">
  <img src="../../../assets/2017-08-24-help-my-provider-is-down/keep-calm.png" alt="Keep calm and use Notif.me">
</p>

*Not developing in Node.js? You can still run it in a micro-service (see [notifme-sdk-queue-rabbitmq](https://github.com/notifme/notifme-sdk-queue-rabbitmq) to get an example).*

## Use a fallback provider

If you're using only one provider, it's about time to open a second account and use it in case the first one fails. We wanted to make that very easy with [notifme-sdk](https://github.com/notifme/notifme-sdk):

```shell
$ yarn add notifme-sdk
```

```javascript
import NotifmeSdk from 'notifme-sdk'

new NotifmeSdk({
  channels: {
    sms: {
      // Use Nexmo and fallback to Twilio in case of failure
      multiProviderStrategy: 'fallback',
      providers: [{
        type: 'nexmo',
        apiKey: 'xxxxx',
        apiSecret: 'xxxxx'
      }, {
        type: 'twilio',
        accountSid: 'xxxxx',
        authToken: 'xxxxx'
      }]
    }
  }
})

notifmeSdk.send({
  sms: {
    from: 'Notifme',
    to: '+15000000001',
    text: 'Hello, how are you?'
  }
})
```

That should cover almost any case you will encounter :thumbsup:

## Going even further

If all your notifications are critical for your business, here are two more things you need to consider:

### 1. Handle fallback failure

This is for the slight possibility of having all your providers failing:

```javascript
const request = {
  sms: {from: 'Notifme', to: '+15000000001', text: 'Hello'}
}

notifmeSdk.send(request).then((result) => {
  if (result.status === 'error') {
    /*
     * Here is a (non-exhaustive) list of what you can do:
     * 1. Try another channel:
     *    notifmeSdk.send({email: {...}})
     * 2. Construct the new request with the failing channels
     *    and enqueue it to a delayed queue to retry it later.
     */
  }
})
```

### 2. Integrating your providers' webhooks

You should also handle error events happening after a provider accepted your request. For example if you send an email and get a soft bounce because your user's inbox is full, you can try to send a web push notification or a SMS instead.

*This is not possible yet with Notif.me SDK but this is definitely something we'd like to work on.*

## Conclusion

If you :heart: this project, you can [star our GitHub repository](https://github.com/notifme/notifme-sdk) and [stay tuned](https://twitter.com/notif_me) for the next episode :)
