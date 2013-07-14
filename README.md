# symfio-contrib-nodemailer

> Email sender plugin.

[![Build Status](https://travis-ci.org/symfio/symfio-contrib-nodemailer.png?branch=master)](https://travis-ci.org/symfio/symfio-contrib-nodemailer) [![Dependency Status](https://gemnasium.com/symfio/symfio-contrib-nodemailer.png)](https://gemnasium.com/symfio/symfio-contrib-nodemailer)

## Usage

```coffee
symfio = require "symfio"

container = symfio "example", __dirname

container.set "mailTransportType", "smtp"

container.set "mailTransportOptions",
  service: "gmail"
  auth:
    user: "example@gmail.com"
    pass: "password"

container.inject require "symfio-contrib-nodemailer"

container.inject (sendMail, container) ->
  sendMail
    to: "test@example.com"
    subject: "Subject"
    text: "Body"
  .then ->
    console.log "Mail sent"
  .then null, (err) ->
    console.log err
  .then ->
    container.get "mailTransport"
  .then (mailTransport) ->
    mailTransport.close()
```

## Configuration

### `mailTransportType`

Default is `sendmail`.

### `mailTransportOptions`

Nodemailer transport options.

## Services

### `mailTransport`

Configured nodemailer transport.

### `sendMail`

Wrapped `mailTransport.sendMail`. Returns promise.
