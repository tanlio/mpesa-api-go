# MPESA Golang API Wrapper  [![CircleCI](https://circleci.com/gh/AndroidStudyOpenSource/mpesa-api-go.svg?style=shield)](https://circleci.com/gh/AndroidStudyOpenSource/mpesa-api-go) [![Maintainability](https://api.codeclimate.com/v1/badges/54dcfdfde1daf230516f/maintainability)](https://codeclimate.com/github/AndroidStudyOpenSource/mpesa-api-go/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/54dcfdfde1daf230516f/test_coverage)](https://codeclimate.com/github/AndroidStudyOpenSource/mpesa-api-go/test_coverage)


The wrapper provides convenient access to the [Safaricom MPESA Daraja API](https://developer.safaricom.co.ke/apis-explorer) for applications written in server-side Golang. :rocket:

## Installing
You can install the package by running:

```
go get github.com/tanlio/mpesa-api-go
```

## Usage
The package needs to be configured with your **appKey** and **appSecret** which can be obtained from Safaricom.

```
const (
	appKey = "YOUR_APP_KEY"		    
	appSecret = "YOUR_APP_SECRET"	   
)
```

The following examples with show you how to make requests to the various api's available.

### MPESAExpress (Formerly STKPush)
This api allows you to do Lipa Na M-Pesa payment using STK Push. This is a simple example:
```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.Simulation(mpesa.Express{
		BusinessShortCode: "",
		Password:          "",
		Timestamp:         "",
		TransactionType:   "",
		Amount:            0,
		PartyA:            "",
		PartyB:            "",
		PhoneNumber:       "",
		CallBackURL:       "",
		AccountReference:  "",
		TransactionDesc:   "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}

```

### C2B
This api allows you to register C2B Callback URLs to Safaricom, and also Simulate a C2B Transaction in ```Sandbox```

This is a simple demo to show how to register C2B Callback URL:

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.C2BRegisterURL(mpesa.C2BRegisterURL{
		ShortCode:       "",
		ResponseType:    "",
		ConfirmationURL: "",
		ValidationURL:   "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}

```
To simulate a C2B Request, use this simple example:

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.C2BSimulation(mpesa.C2B{
		ShortCode:     "",
		CommandID:     "",
		Amount:        "",
		Msisdn:        "",
		BillRefNumber: "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}
```

### B2C
This api allows you to do M-Pesa Transaction from company to client.

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

    var initiatorPassword = ""
	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}
    
    securityCredential, err := svc.GetSecurityCredential(initiatorPassword)
    if err != nil {
        panic(err)
    }

	res, err := svc.B2CRequest(mpesa.B2C{
		InitiatorName:      "",
		SecurityCredential: securityCredential,
		CommandID:          "",
		Amount:             0,
		PartyA:             "",
		PartyB:             "",
		Remarks:            "",
		QueueTimeOutURL:    "",
		ResultURL:          "",
		Occassion:          "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}
```

### B2B
This api allows you to do M-Pesa Transaction from one company to another.

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.B2BRequest(mpesa.B2B{
		Initiator:              "",
		SecurityCredential:     "",
		CommandID:              "",
		SenderIdentifierType:   "",
		RecieverIdentifierType: "",
		Remarks:                "",
		Amount:                 0,
		PartyA:                 "",
		PartyB:                 "",
		AccountReference:       "",
		QueueTimeOutURL:        "",
		ResultURL:              "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}

```

### Account Balance
This api allows you to do balance inquiry.

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.BalanceInquiry(mpesa.BalanceInquiry{
		Initiator:          "",
		SecurityCredential: "",
		CommandID:          "",
		PartyA:             "",
		IdentifierType:     "",
		Remarks:            "",
		QueueTimeOutURL:    "",
		ResultURL:          "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}
```

### Transaction Status
This api allows you to check the status of transaction.

### Reversal
This api allows you to do a transaction reversal

```go
package main

import (
	"log"
	"github.com/AndroidStudyOpenSource/mpesa-api-go"
)

const (
	appKey    = ""
	appSecret = ""
)

func main() {

	svc, err := mpesa.New(appKey, appSecret, mpesa.SANDBOX)
	if err != nil {
		panic(err)
	}

	res, err := svc.Reversal(mpesa.Reversal{
		Initiator:              "",
		SecurityCredential:     "",
		CommandID:              "",
		TransactionID:          "",
		Amount:                 0,
		ReceiverParty:          "",
		ReceiverIdentifierType: "",
		QueueTimeOutURL:        "",
		ResultURL:              "",
		Remarks:                "",
		Occassion:              "",
	})

	if err != nil {
		log.Println(err)
	}
	log.Println(res)

}
```

### Contributing

We’re glad you’re interested in MPESA Daraja Golang SDK, and we’d love to see where you take it. If you would like to contribute code to this project you can do so through GitHub by Forking the Repository and creating a Pull Request.

When submitting code, please make every effort to follow existing conventions and style in order to keep the code as readable as possible. We look forward to you submitting a Pull Request.

Use [gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows#gitflow-workflow).
Always tag releases to `develop` and `master`.

Thanks, and please do take it for a joyride!

### License

```text
MIT License

Copyright (c) 2018 Android Study Open Source

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
```
