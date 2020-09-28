# Introduction
[Instructions on how to integrate the widget are here.](https://docs.onramper.dev/widget/)

Onramper allows you to let your users buy crypto directly on your website or app. Onramper is a fiat-to-crypto gateway aggregator, which implements all major gateways in a single solution. This allows businesses to get global coverage of supported countries, payment methods, cryptocurrencies and fiat currencies. At the same time, businesses are free to implement their [own fees](#fees) on every user transaction.

Onramper consist of a [widget](#the-widget) and an [API](#the-api). The API is, as of yet, unavailable. 

## Integrated fiat gateways
Currently, the integrated gateways are:  
· <a href="https://moonpay.io" target="_blank">Moonpay</a>  
· <a href="https://sendwyre.com" target="_blank">Wyre (soon)</a>  
· <a href="https://www.coinify.com/" target="_blank">Coinify (soon)</a>  
· <a href="https://cryptocoin.pro" target="_blank">Cryptocoin.pro (soon)</a>  

We'll continue to contract with and integrate additional gateways. We'll also be adding an offramp soon (allowing users to sell crypto for fiat).


# The Widget
The widget can be easily implemented on your app/wallet, so you can focus on getting users, instead of having to integrate multiple fiat gateways yourself. The widget can be integrated in as little as 5 minutes. It is possible to customize the widget to only show certain currencies, payment methods, etc. You can also automatically insert the user's public key, and change the widget's colours to match your site/app.

· <a href="https://widget.onramper.com" target="_blank">Try the widget for yourself.</a>   
· [Customize and integrate the widget.](https://docs.onramper.dev/widget/)   
· [Technical overview of how the widget works](https://docs.onramper.dev/readmewidget/)

# The API
**The API is currently unavailable.**
Onramper can soon be implemented by connecting to our API. As such, businesses will be able to integrate Onramper however they want. Connecting by API is more work, but allows you to build your own UX/UI.

· [See the reference list of API endpoints](https://docs.onramper.dev/API-Reference/)  
· [API wrappers (under development)](https://docs.onramper.dev/apicontext/)

# Fees
Users pay fees for the conversion to the chosen fiat gateway. Additionally, they'll pay 0.75% of the tx to Onramper. However, Onramper is able to get lower rates from gateways that offset this fee in many cases. 

You can also add your own fees on top of every transaction. For this you'll need a special API key provided by Onramper, which is provided <a href="https://forms.gle/9SQXhhyxHFZvBJ7J6" target="_blank">after completing this form</a>.

