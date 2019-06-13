
# react-native-google-pay
[![react-native version](https://img.shields.io/badge/react--native-0.41-0ba7d3.svg?style=flat-square)](https://github.com/facebook/react-native/releases/tag/v0.41.0)
![npm](https://img.shields.io/npm/dw/react-native-google-pay.svg?style=flat-square)
[![npm (tag)](https://img.shields.io/npm/v/react-native-google-pay/latest.svg?style=flat-square)](https://github.com/busfor/react-native-google-pay/tree/master)

Accept Payments with Google Pay for React Native apps.

<div>
<img width="280px" src="emulator.gif" />
</div>

---

## Getting started

`$ yarn add react-native-google-pay`

### Mostly automatic installation

`$ react-native link react-native-google-pay`

### Manual installation


#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.busfor.RNGooglePayPackage;` to the imports at the top of the file
  - Add `new RNGooglePayPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-google-pay'
  	project(':react-native-google-pay').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-google-pay/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-google-pay')
  	```

#### Enable Android Pay in your Manifest

To enable Google Pay in your app, you need to add the following Google Pay API meta-data element to the `<application>` element of your project's AndroidManifest.xml file.

```xml
<meta-data
    android:name="com.google.android.gms.wallet.api.enabled"
    android:value="true" />
```

## Usage
```javascript
import { GooglePay } from 'react-native-google-pay';

const requestData = {
  cardPaymentMethod: {
    tokenizationSpecification: {
      type: 'PAYMENT_GATEWAY',
      gateway: 'example',
      gatewayMerchantId: 'exampleGatewayMerchantId',
    },
    cardNetworks,
  },
  transaction: {
    totalPrice: '10',
    totalPriceStatus: 'FINAL',
    currencyCode: 'USD',
  },
  merchantName: 'Example Merchant',
}

// Set the environment before the payment request
GooglePay.setEnvironment(GooglePay.ENVIRONMENT_TEST)

// Check if Google Pay is available
GooglePay.isReadyToPay(cardNetworks)
  .then(() => {
    // Request payment token
    GooglePay.requestPayment(requestData)
      .then((token: string) => {
	    // Send a token to your payment gateway
	  })
  })
```

## Demo
You can run the demo by cloning the project and running:

`$ yarn demo`