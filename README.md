# Node SerialPort-GSM

SerialPort-GSM - A library for the communication with GSM modems like sending and receiving SMS messages.

[![NPM](https://nodei.co/npm/@remimomprive/serialport-gsm-typescript.png)](https://npmjs.org/package/@remimomprive/serialport-gsm-typescript)

## Install

```bash
npm i @remimomprive/serialport-gsm-typescript
```

## Usage

Usage in JavaScript/TypeScript (with ES Modules):

```typescript
import { Modem, SerialPortCommunicator } from '@remimomprive/serialport-gsm-typescript';

// Initialize a SerialPortCommunicator. For more options take a look at the full documentaion
const serialPortCommunicator = new SerialPortCommunicator('COM4');

// Initalization of the modem. For more options take a look at the full documentaion
const myModem = new Modem(serialPortCommunicator);

// You can listen to different events
myModem.on('onWriteToModem', (data) => console.log('>:', data.replace(/\n|\r/g, '')));
myModem.on('onDataReceived', (data) => console.log('<:', data.replace(/\n|\r/g, '')));

// Do whatever you want
async function start() {
  await myModem.open();

  console.log('.checkModem()', await myModem.checkModem());
  console.log('.getSignalInfo()', await myModem.getSignalInfo());
  console.log('.getRegisteredNetwork()', await myModem.getRegisteredNetwork());
  console.log('.getAvailableNetworks()', await myModem.getAvailableNetworks());
  console.log('.checkSimMemory()', await myModem.checkSimMemory());
  console.log('.getProductSerialNumber()', await myModem.getProductSerialNumber());
  console.log('.getOwnNumber()', await myModem.getOwnNumber());
  console.log('.getSimInbox()', await myModem.getSimInbox());
  console.log('.sendSms()', await myModem.sendSms('+XXXXXXXXX', 'Hello, Zap here!'));

  await myModem.close();
}

start();
```

---

## 🤝 Contributing

Contributions, issues and feature requests are welcome! Feel you free to check [issues page](https://github.com/@remimomprive/serialport-gsm-typescript/issues) or create a [pull request](https://github.com/@remimomprive/serialport-gsm-typescript/pulls). We are happy about collaboration on this project.
