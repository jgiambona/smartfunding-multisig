Ethereum Multisig
=================

This repository implements an Ethereum smart contract
(`Multisig2of3`) which requires signed messages from 2/3 members
of a multisig cold wallet with individual keys stored on
[Trezor] or [Ledger] hardware wallets.

Command-line scripts are also provided (see the `scripts` directory)
for developers who want to create and spend from the smart contract
programatically.

Running Local dApp
------------------

To access the dApp locally, download or clone this repository.

Once downloaded you can use access the dApp in two ways:

1. Navigate with your browser to the file `public/index.html` inside
   this repository.  This option is easier but somewhat less secure.
2. Launch a local webserver and point your browser to
   https://localhost:8435.  This option is more secure but requires a
   local [NPM] installation and using the
   command-line -- see the [section below](#local-webserver) for
   instructions.

Which you choose will depend on which Ethereum node you are using and
how you've configured it:

* MetaMask -- For security reasons, option (1) is [not allowed][metamask file]
  by MetaMask -- you **must** use option (2) and launch a local webserver.
* Geth
  * To use option (1) and navigate with your browser to the file
    `public/index.html` you will need to set `--rpccorsdomain null`
    (this is why this option is less secure).
  * To use option (2) and point your browser to
    `https://localhost:8435` you will need to set `--rpccorsdomain
    https://localhost:8435`.    
    
    
Launching a Local Webserver
-----------------------------

This repository also comes with a simple webserver which provides a
more secure alternative to directly browsing to the
`public/index.html` file.  (This is required for MetaMask and Ledger).

To launch the local webserver you will need
[NPM] to be installed locally as well as the
[make] program.

To install dependencies and launch the server, open a shell in this
repository's directory and run:

```
$ make dependencies
$ make server
```

Now browse to https://localhost:8435 to see the dApp. You will have to accept
an insecure connection warning.


Compiling & Testing the Contract
--------------------------------

Once dependencies are installed, you can compile the contract.

```
$ make contract
```

and run its unit tests

```
$ make test
```

We are using the [Truffle framework] so
`truffle` commands are available.  To make them easier to run, you
should update your `PATH` variable or set a shell alias.  You can also just run

```
$ source environment.sh
```

to do all of this for you.  Now you can run the `truffle` commands, e.g. - 

```
$ truffle compile
```

Command-Line Scripts
--------------------

This repository also comes with the command-line Python and Node scripts for
interacting with the smart contract:

* `scripts/export_ethereum_address` --
    exports an Ethereum address from a local Trezor.
* `scripts/ledger/ledger-address.js` --
    exports an Ethereum address from a local Ledger.
* `scripts/create_ethereum_multisig` --
    creates a new instance of the smart contract.
* `scripts/ethereum_multisig_spend_unsigned_data` --
    return the unsigned data used for a spend
* `scripts/export_ethereum_multisig_spend_signature` --
    export a signed spend from a local Trezor.
* `scripts/ledger/ledger-sign-message.js` --
    export a signed spend from a local Ledger.
* `scripts/spend_ethereum_multisig` -- broadcast a spend transaction
