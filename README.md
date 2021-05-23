# Paylense API Python SDK</h1>

<strong>Payment gateway for african businesses</strong>

<div>
  Join our active, engaged community: <br>
  <a href="https://spectrum.chat/paylense-api-sdk/">Spectrum</a>
  <br><br>
</div>


[![Build Status](https://travis-ci.com/winopay/paylense-python-sdk.svg?branch=master)](https://travis-ci.com/winopay/paylense-python-sdk)
[![Latest Version](https://img.shields.io/pypi/v/tox-travis.svg)](https://badge.fury.io/js/paylense-python-sdk)
[![Coverage Status](https://coveralls.io/repos/github/winopay/paylense-python-sdk/badge.svg?branch=master)](https://coveralls.io/github/winopay/paylense-python-sdk?branch=master)
[![Join the community on Spectrum](https://withspectrum.github.io/badge/badge.svg)](https://spectrum.chat/paylense-api-developers/)


# Usage

## Installation

Add the latest version of the library to your project using pip:

```bash
 $ pip install paylense-sdk
```

This library supports Python 3.4+ (PyPy supported)

# Account details

## Getting environment API user

Next, we need to get the `APP-ID`, `username` and `password` for use in the product. You can get these details from `https://dashboard.paylense.com/register`.

The redentials in the sandbox environment can be used straight away. In production, the credentials are provided for you after KYC requirements are met.

## Configuration

Before we can fully utilize the library, we need to specify global configurations. The global configuration must contain the following:

* `PAYLENSE_ENVIRONMENT`: Optional enviroment, either "sandbox" or "production". Default is 'sandbox'
* `PAYLENSE_APP_ID`: The unique application identity for your app
* `PAYLENSE_USERNAME`: Username used for authentication
* `PAYLENSE_PASSWORD`: Password used for authentication

The full list of configuration options can be seen in the example below:

 ```python
 config = {
    "PAYLENSE_ENVIRONMENT": os.environ.get("PAYLENSE_ENVIRONMENT"),
    "PAYLENSE_APP_ID": os.environ.get("PAYLENSE_APP_ID"),
    "PAYLENSE_USERNAME": os.environ.get("PAYLENSE_USERNAME"),
    "PAYLENSE_PASSWORD": os.environ.get("PAYLENSE_PASSWORD"),
}
```

## Collections
Used for receiving money

You can create a collections client with the following:

```python
import os
from paylense.collections import Collections

client = Collections()
```

### Methods

1. `requestToPay`: This operation is used to request a payment from a consumer (Payer). The payer will be asked to authorize the payment. The transaction is executed once the payer has authorized the payment. The transaction will be in status PENDING until it is authorized or declined by the payer or it is timed out by the system. Status of the transaction can be validated by using `getTransactionStatus`.

2. `getTransaction`: Retrieve transaction information using the `transactionId` returned by `requestToPay`. You can invoke it at intervals until the transaction fails or succeeds. If the transaction has failed, it will throw an appropriate error.

### Sample Code

```python
import os
from paylense.collections import Collections

client = Collections()

client.requestToPay(
    mobile="256772123456", amount="600", processing_number="123456789", narration="dd")
```

## Disbursements

Used for sending money to users

You can create a disbursements client with the following

```python
import os
from paylense.disbursements import Disbursements

client = Disbursements()
```

### Methods

1. `transfer`: Used to transfer an amount from the owner’s account to a payee account. Status of the transaction can be validated by using the `getTransactionStatus` method.

2. `getTransactionStatus`: Retrieve transaction information using the `transactionId` returned by `transfer`. You can invoke it at intervals until the transaction fails or succeeds.

#### Sample Code

```python
import os
from paylense.disbursements import Disbursements

client = Disbursements()

client.transfer(amount="600", mobile="256772123456", processing_number="123456789", narration="dd")

```

### Developer
We use `tox` to automate our tests. You can run the test using

```python
tox
```
Thank you.
