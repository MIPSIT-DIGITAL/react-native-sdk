## Installation

```  bash 
npm install react-native-sdk
```
## Usage

#### 1. import required classes

``` javascript
import {
	StartPayment,
	Amount,
	MerchantDetails,
	MerchantCredentials,
	Currency,
} from "mu.mips.react-native-sdk";
```
#### 2. create order data and merchant data models
```Javascript
const orderID = "YOUR_ORDER_ID";

const amount = new Amount(Currency.Mauritian_Rupee, 100);
// replace currency and amount with required values

const detail = new MerchantDetails(
	"XXXXX", //sIdMerchant
	"XXXXX", //salt
	"XXXXX", //sCipherKey
	"XXXXX", //id_entity
	"XXXXX", //id_operator
	"XXXXX", //operator_password
);

const cred = new MerchantCredentials(
	"XXXXX", //username
	"XXXXX". //password
);
// above info will be provided by MIPS admin
```
#### 3. Finally call `StartPayment` function to start the payment flow
``` Javascript
StartPayment(
	detail , cred , amount , orderID
).then((paymentMode) => {
	console.log("payment success with payment mode " + paymentMode)
}).catch( (error) => {
	console.log("payment failed with error " , error)
})

// StartPayment will show the payment screen and notify once payment status changes 
```

#### for eg:-  we can call `StartPayment` on click of a button

``` javascript
export default function App() {
	return (
		<View style={styles.container}>
			<Button onPress={() => {
				console.log("payment flow started")
				StartPayment(
					detail , cred , amount , orderID
				).then((paymentMode) => {
					// payment completed
				}).catch( (error) => {
					// payment failed
				})
			}} title="click to pay" color="#841584" />
		</View>
	);
}
```