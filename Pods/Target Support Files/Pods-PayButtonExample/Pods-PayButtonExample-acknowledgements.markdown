# Acknowledgements
This application makes use of the following third party libraries:

## Alamofire

Copyright (c) 2014-2020 Alamofire Software Foundation (http://alamofire.org/)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


## DynamicBlurView

The MIT License (MIT)

Copyright (c) 2015 Kyohei Ito

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.



## EVReflection

MIT 3 License

Copyright (c) 2015, EVICT B.V.
All rights reserved.
http://evict.nl, mailto://edwin@evict.nl

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:
* Redistributions of source code must retain the above copyright
notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright
notice, this list of conditions and the following disclaimer in the
documentation and/or other materials provided with the distribution.
* Neither the name of EVICT B.V. nor the
names of its contributors may be used to endorse or promote products
derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL <COPYRIGHT HOLDER> BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


## MOLH

MIT License

Copyright (c) 2017 Moath othman

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


## PayButtonNumo

## PaySky Button SDK

The purpose of this SDK to help programmers to use PaySky payment SDK for IOS .

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them

```
1-COCOPODS installed on your machine   .
2-Xcode
3-Create new IOS project in xcode to use SDK or if you have created a project before with swit
```

### Installing

A step by step that tell you how to get our SDK in your project.

```
1- open your xcode project.
2- in your project in Podfile in project level  add :-
pod 'PayButton'
3- open your terminal in project path and write this command:-
(for first try)
- pod deintegrate
- pod update
(for second try)
- pod install


### Using SDK

```
in order to use our SDK you should get merchant id and Terminal id from our company.

1-import PayButton
2 ??? create a new instance from PayButton:-  

 let paymentViewController = PaymentViewController ()

you need to just pass some parameters to PayButton class instance :-
  1-Merchat id.
  2-Terminal id.
  3-Payment amount.
  4-Currency code [Optional].
  5-merchant secure hash.
  6-transaction Reference Number.
  
Note That:-
you shoud keep your secure hash and merchant id and terminal id with encryption before save them in storage if you want.

Example:-


        paymentViewController.amount =  "amount"  // Amount
        paymentViewController.delegate = self // PaymentDelegate
        paymentViewController.mId = "merchantId" // Merchant id
        paymentViewController.tId = "terminalId" // Terminal  id
        paymentViewController.Currency = "currencyCode" // Currency Code [Optional]
        paymentViewController.refnumber = "reference number""  // unique transaction reference number.
        paymentViewController.Key = "Merchant secure hash" // merchant secrue hash
        paymentViewController.pushViewController()

       
2 - in order to create transaction call back in deleget PaymentDelegate:-

    implete deleget on your ViewController
    class ViewController: UIViewController, PaymentDelegate  {\
        var receipt: TransactionStatusResponse = TransactionStatusResponse()

        func finishSdkPayment(_ receipt: TransactionStatusResponse) {
        self.receipt = receipt
        if receipt.Success {

            LabeResoinse.setTitle("Transaction completed successfully, click here to show callback result", for: .normal)
            
        }else {
            LabeResoinse.setTitle("Transaction has been failed click to callback callback ", for: .normal)


            
        }
    }


    }


to create transaction in our sdk you just call createTransaction method and pass to it
PaymentTransactionCallback listener to call it after transaction.
this listener has 2 methods:-

  1 - finishSdkPayment method
      this method called in case transaction success by card payment with SuccessfulCardTransaction object.
      SuccessfulCardTransaction object from create transaction listener contains:-
      NetworkReference variable that is reference number of transaction.
      AuthCode variable
      ActionCode variable.
      ReceiptNumber variable.
      amount variable.
      
  2 - finishSdkPayment method 
      this method is called if customer make a wallet transaction with SuccessfulWalletTransaction object.
      SuccessfulWalletTransaction object from create transaction listener contains:-
      NetworkReference variable that is reference number of transaction.
      amount variable.
      


  
Example:- 

           func finishSdkPayment(_ receipt: TransactionStatusResponse) {
         if receipt.Success   // will be true if transaction success 
         {
          print(receipt.NetworkReference)
         }else{
          print(receipt.Message) // resonse of error

         }
    }

```


## Deployment

1-Before deploy your project live ,you should get a merchant id and terminal id from our company .
2-you should keep your merchant id and terminal id secured
in your project, encrypt them before save them in project.

## Built With

* [Alamofire](https://github.com/Alamofire/Alamofire)  
* [EVReflection](https://github.com/evermeer/EVReflection)  


## Authors

**PaySky Company** - (https://www.paysky.io)

## Sample Project
**https://github.com/payskyCompany/payButtonIOS.git**


## PayCardsRecognizer

MIT License

Copyright (c) 2017 faceterteam

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


## PopupDialog

Copyright (c) 2016 Orderella Ltd. (http://orderella.co.uk)
Author - Martin Wildfeuer (http://www.mwfire.de)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

Generated by CocoaPods - https://cocoapods.org
