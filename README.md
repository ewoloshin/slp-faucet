# SOUR SLP Faucet

This project is an example of an SLP faucet website.  The site allows users to enter their SLP address and the server-side process will send the user's address the token quantity specified within the environment variables (i.e., per `TOKENQTY` and `TOKENID`).  

SOUR SLP Faucet is live at: [http://sour-faucet.ddns.net](http://sour-faucet.ddns.net)

## Faucet Capacity

This faucet can service 450 uses per block (i.e., 25 txn limit/block x 18 addresses = 450).  The server application allows the faucet admin to automatically distribute the tokens and BCH evenly across the first 18 addresses which are located on the `m/44'/245'/0'/0/X` HD path, where `X` is the address indecies 0 to 17.  The admin can instantiate this automatic distribution by entering the `DISTRIBUTE_SECRET` environment variable into the site's address input field.

NOTE: You will need to wait 1 block confirmation after distribution step before the faucet will be able to be used.  This is because address selection is based on finding the first address with a unconfirmed balance of 0 BCH.

## Setup

* Use Electron Cash SLP or other SLP wallet to store faucet token & BCH coins, then use the mnemonic for that wallet for the faucet in the `MNEMONIC` environmental variable.

* Create a new `.env` file with the following environment variables:
```
MNEMONIC=______
TOKENID=_______
TOKENQTY=______
DISTRIBUTE_SECRET=______
PORT=______
```

## Run the web app locally:

```
npm install
tsc
node server.js
```

### *** Note - there has been recent issues running with the bitbox-sdk module. As a workaround, go into the below two files and change one line in each.

In file - 
node_modules/bitbox-sdk/lib/Crypto.ts

Change line 1 - 

import * as randomBytes from "randombytes" 

To - 

import randomBytes from "randombytes"


In file - 
node_modules/bitbox-sdk/lib/Mnemonic.ts

Change line 5 - 

import * as randomBytes from "randombytes"

To -

import randomBytes from "randombytes"


## Build Source

If you want to modify the source (i.e., the `*.ts` files), you will need to rebuild using `tsc` before running the app.  TypeScript needs to be installed globally via `npm install -g typescript`.
