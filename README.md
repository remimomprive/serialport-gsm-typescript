# Node SerialPort-GSM

## Intro

SerialPort-GSM is a simplified plugin for communicating with gsm modems. (Primarily for sms)
***
## Table of Contents

* [Installation](#installation-instructions)
* [Usage](#usage)
* [License](#license)

***
## Installation Instructions

```
npm install serialport-gsm
```

## Usage

#### List Available Ports
```js
let serialportgsm = require('serialport-gsm')

serialportgsm.list((err, result) => {
    console.log(result)
})
```

#### Opening a Port
Call other functions after the port has been opened.
`open(path, options, callback)`
```js
let serialportgsm = require('serialport-gsm')
let modem = serialportgsm.Modem()
let options = {
    baudRate: 115200,
    dataBits: 8,
    parity: 'none',
    stopBits: 1,
    flowControl: false,
    xon: false,
    rtscts: false,
    xoff: false,
    xany: false,
    buffersize: 0
}

modem.open('COM', options, callback[Optional])
```
#### Initialize Modem
This function starts the modem. (If your port fails to work or does not respond to commands, don't forget to call `initializeModem` after opening the port.)
```
modem.on('open', data => {
    modem.initializeModem(callback[optional])
})
```

#### Set Modem Mode
`setModemMode(callback, type)`
* type can be `'PDU'` or `'SMS'`
```
modem.on('open', data => {
    modem.setModemMode(callback, 'PDU')
})
```

#### Send Message
Sends sms.
`sendSMS(recipient, message, alert, callback)`
* alert parameter is boolean
`true` - send as class 0 message(flash message)
`false` - send as a normal sms
```
modem.sendSMS('0999XXXXX19', 'Hello there Zab!', true, callback)
```
#### Delete All Sim Messages
```
modem.deleteAllSimMessages(callback)
```

#### Get Modem Serial
```
modem.getModemSerial(callback)
```

#### Get Network Signal
```
modem.getNetworkSignal(callback)
```

#### Get Network Signal
```
modem.getNetworkSignal(callback)
```
#### Execute AT Command
```
modem.executeCommand(callback, priority, timeout)
```

## Other Usage 
### Event Listeners
#### open
```
modem.on('open', result => { //do something })
```

#### close
```
modem.on('close', result => { //do something })
```

#### error
```
modem.on('error', result => { //do something })
```

#### onSendingMessage
```
modem.on('onSendingMessage', data => { status, request, data })
```

#### onNewMessageIndicator
```
modem.on('onNewMessageIndicator', data => { sender, timeSent })
```

#### onNewMessage
```
modem.on('onNewMessage', messageDetails)
```

## SerialPort
Access base serialport. Please refer to [***SerialPort@7.1.1***](https://www.npmjs.com/package/serialport/v/6.2.2) for documentation
```
modem.port
```

## License
SerialPort-GSM is [ISC licensed](LICENSE) and all it's dependencies are MIT or BSD licensed.
