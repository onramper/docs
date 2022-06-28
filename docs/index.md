# Introduction
[Instructions on how to integrate the widget are here.](./widget.md)

Onramper allows you to let your users buy crypto directly on your website or app. Onramper is a fiat-to-crypto gateway aggregator, which implements all major gateways in a single solution. This allows businesses to get global coverage of supported countries, payment methods, cryptocurrencies and fiat currencies. At the same time, businesses are free to implement their [own fees](#fees) on every user transaction.

Onramper consist of a [widget](#the-widget) and an [API](#the-api).

## Integrated fiat gateways
Currently, the integrated gateways are:  
* <a href="https://moonpay.io" target="_blank">Moonpay</a>  
* <a href="https://sendwyre.com" target="_blank">Wyre</a>  
* <a href="https://xanpool.com/" target="_blank">Xanpool</a>  
* <a href="https://mercuryo.io/" target="_blank">Mercuryo</a>  
* <a href="https://www.coinify.com/" target="_blank">Coinify</a>  
* <a href="https://www.indacoin.com/" target="_blank">Indacoin</a>  
* <a href="https://utorg.pro/" target="_blank">Utorg</a>  
* <a href="https://btcdirect.eu/en-gb/" target="_blank">BTCDirect (live Soon)</a>  
* <a href="https://ramp.network/" target="_blank">Ramp Network (live Soon)</a>  
* <a href="https://transak.com/" target="_blank">Transak (live Soon)</a>  

We'll continue to contract with and integrate additional gateways. We'll also be adding an offramp soon (allowing users to sell crypto for fiat).  


# The Widget
The widget can be easily implemented on your app/wallet, so you can focus on getting users, instead of having to integrate multiple fiat gateways yourself. The widget can be integrated in as little as 5 minutes. It is possible to customize the widget to only show certain currencies, payment methods, etc. You can also automatically insert the user's public key, and change the widget's colours to match your site/app.

· <a href="https://widget.onramper.com" target="_blank">Try the widget for yourself.</a>  
· <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform" target="_blank">Sign up for an production-ready API key.</a>  
· [Customize and integrate the widget.](./widget.md)  
· [Technical overview of how the widget works](https://github.com/onramper/widget/blob/dev/README.md)  
  
<!---
# The API
Onramper can be implemented by connecting to our API. As such, businesses will be able to integrate Onramper however they want. Connecting by API is more work, but allows you to fully build your own UX/UI. Note that our widget is highly customizable by itself, and integration of the widget ensures you instantly get every update we do on your integration.

· <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform" target="_blank">Sign up for an production-ready API key.</a>  
· [See the reference list of API endpoints](./API-Reference.md)  
· API wrappers (under development)  
--->
  
# Fees
Users pay fees for the conversion to the chosen fiat gateway. Additionally, end-users pay 1% of the tx to Onramper. However, end-users still pay less in fees than without Onramper as we ensure the lowest fee gateway will always be available for their transactions, which usually saves users far more than 1%. Additionally, Onramper procures lower rates than normally charged by gateways. In most cases, Onramper's fee is not added on top of the gateways' fee. 

You can also add your own fees on top of every transaction. For this you'll need to use a special API key provided by us. Please fill in our <a href ="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform" taget="_blank">client onboarding form.</a>

