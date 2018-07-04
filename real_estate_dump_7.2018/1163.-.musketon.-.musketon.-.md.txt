<h3 align="center">
  <img src="https://raw.githubusercontent.com/musketon/musketon/master/docs/res/musketon.png" alt="logo" width=400 />
</h3>

<hr />

[![](https://img.shields.io/github/release/musketon/musketon.svg?style=flat)](https://github.com/musketon/musketon/releases)
[![](https://img.shields.io/badge/discord-@florisvdg-blue.svg?style=flat)](https://discord.gg/DtzSb2Z)

<br />

🎉[**_Proud award of merit ($15,000) winner in the 1st NEO / Microsoft Developer Competition_**](https://neo.org/awards.html) 🎉

<br />

`musketon` gives you full control of who you grant access to your most personal data. You can authorize third parties to access specific data points about you, set an access expiry moment, arbitrarily decide to revoke access and follow an audit trail of when and why granted third parties accessed your data. 

You could grant:

* shipping couriers access to your name and home address
* social networks access to your name and birthday
* the municipality access to your name, birthdate, gender and home address
* hotels access to your name, credit card number and dietary preferences
* flight companies access to your name and passport number
* the tax collection agency access to your bank account and crypto wallet addresses
* your landlord and real estate agent access to your name, salary payslip and employment contract
* ....many, many more use cases

Feeling like there's a third party that does not need your data anymore? You just revoke their access.

`musketon` is a dApp, powered by the [NEO](https://neo.org/) blockchain. 

## Motivation

People have gotten used to going around filling out forms on nearly any website that asks for it, often not realizing that the website then forever has their data. The moment you click _submit_, you lose control about the further destinations of this data. `musketon` aims to make these data exchanges much more explicit. 

`musketon` also attaches a license onto every data exchange, which is then logged on the blockchain. Due to the contractual nature of these licenses, a `musketon` grant imposes more consciousness on both sides about the fact that there is a very personal data exchange happening, with potentially serious consequences when misused. 

`musketon` is not only there for the users: businesses need to comply to a rapidly rising number of regulations to protect user data. This forces them to put a lot of effort on meeting these requirements, while that is _not_ their core business. `musketon` offers a standardized way to offload a big part of the burden. 

For EU businesses, incorporating `musketon` means much easier [GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) compliance.

## Entities and terminology

A `musketon` data exchange relies on two parties: 

1. The **user**. The **user** defines **features** about him or herself, and can then **grant** one or more **features** to a **consumer** with a specific usage license.
2. The **consumer**. The **consumer** can then access a **feature**, until the **grant** is revoked or expires. Everytime a **consumer** accesses the data, it will be recorded onto the **audit trail**.

The user can:

* create, read, update and delete their features
* authorize consumers to access to specfic features
* set an expiry moment per grant
* revoke a grant
* inspect the audit trail of a consumer's read operations

The consumer can:

* read out user's granted features as many times as needed, with each time adding a new audit trail record

## Architecture

`musketon` consists of two components:

* the **musketon smart contract**
	* runs on the blockchain
	* serving as the backbone, feature storage and grants ledger
* the **musketon client**
	* runs client-side
	* used by the users and consumers to encrypt and decrypt the user data and invoke the necessary smart contract operations
	* can be incorparated into CLI's, browser extensions, desktop apps, menu bar extensions, etc.

<img src="https://raw.githubusercontent.com/musketon/musketon/master/docs/res/architecture.png" width=800 />

No intermediate server is needed, no intermidate party needs to be trusted, exchanging data is just 'peer-to-NEO-to-peer'.

The stored features are `AES/CBC/PKCS5Padding` encrypted using the user's NEO wallet private key. The stored granted features are `AES/CBC/PKCS5Padding` encrypted using an [elliptic curve Diffie-Hellman](https://en.wikipedia.org/wiki/Elliptic-curve_Diffie%E2%80%93Hellman) shared secret of the user's private key + consumer's public key or the user's public key + consumer's private key.

## Licenses

`musketon` attaches a license to every grant. The license states what the consumer is allowed to do with the granted feature data until the grant expires or is revoked. The are three licenses available (in the future, more licenses could be added):

* **READ** - the most common and most restrictive license. Allows the consumer to request the feature and have a look at it, cache it for 12 hours if needed, but not store it on (long term) disk. This means that after the data is gone, the consumer will have to perform a new read request to see the data again.
* **COPY** _(not yet implemented)_ - allows the consumer to make a copy of the granted feature and store it on disk. The data cannot be shown or shared externally. The copy license also requires the consumer to make sure the data is wiped from disk after the agreed upon expiry time. Revoking is not allowed here, so it is advised to set short expiry times when using the copy license. Useful for hotels needing to store credit card numbers for a couple of days after checkout.
* **EXPOSE** _(not yet implemented)_ - allows the consumer to expose the feature data on the consumer's website. Usage of the expose license should be a rare occurence and should never be used for the more sensitive features. Useful for social networks needing to show the user's name or age.

## Definable features

The features that the user can currently define are:

* name
	* first name
	* last name
* birthdate
	* year
	* month
	* day
* address
	* country
	* province / state
	* city
	* address line 1
	* address line 2
	* postal code
* ...a lot more to be added [in the future](#support-more-features)

There are no required features or fields, the user chooses how complete the data should be. 

> **Note:** `musketon` does _not_ intend to be an authentication nor IDV (identity verification) technology (anwsering the question _are you really who you say you are?_). It is a 100% up to the user to decide how and which features to specify, and `musketon` therefore won't validate or flag you in some way for the data you enter. However, deliberate data misrepresentation will lead into the shipping couriers delivering your package to the wrong address, the flight company rejecting you when boarding a plane, the tax collection agency prosecuting you for tax evasion, etc.


Next to granting defined features, the user can also grant partial features. After all, sharing the city you live in, should not have to make you share your entire address. The grantable features are automatically derived from you defined features. They can consist of a copy of one or more fields, but can also be computationally derived (age from birthdate, initials from name, etc). 

The current grantable features are:

* `name`
* `name.first_name`
* `name.last_name`
* `name.initials`
* `birthdate`
* `birthdate.birthday`
* `birthdate.year`
* `address`
* `address.country`
* `address.city`

## CLI

The `musketon` client comes with a CLI, that can be downloaded from the [GitHub releases](https://github.com/musketon/musketon/releases) page or built from the source code, as described [below](#development).

The CLI requires Java 8 and Node.js 8 (or higher) to be installed. Before running your first command, verify in the `musketon.properties` file contained in the package that the `musketon.neon.nodejs` property for your OS is pointing to the correct Node.js path.

To show the available commands, run:

```
musketon --help
```

To see which features can be defined, run:

```
musketon feature define --help
```

To see the definable components that make up the feature `name`, run:

```
musketon feature define name --help
```

You authenticate by adding your NEO WIF to each command:

```
<command> --me <your neo wif>
```


To define the feature `name`, run:

```
musketon feature define name --first-name Satoshi --last-name Nakomoto --me <wif>
```

Or use the shorthand:

```
musketon feature define name -fn Satoshi -ln Nakomoto --me <wif> 
```

> _**Note**: the writing actions (define, delete, revoke, authorize, etc) take a quite a bit longer than the reading actions, due to the musketon client waiting for blockchain confirmations and some write actions needing to do multiple invocations._

If you want to see more of what's happening in the background (particularly useful for the write actions), add the debug flag to the command:

```
--debug
```

To see the defined feature, run:

```
musketon feature get name --me <wif>
```

To delete it, run:

```
musketon feature delete name --me <wif>
```

To authorize a consumer with the consumer's public key and a grant expiry of 14 days:

```
musketon grant authorize name --me <wif> --consumer <consumer public key> --expiry 14
```

Or alternatively use the `--indefinite` flag:

```
musketon grant authorize name --me <wif> --consumer <consumer public key> --indefinite
```

To see the grant, run:

```
musketon grant get name --me <wif> --consumer <consumer public key>
```

To see the full grant license written out, add the `--license` flag

```
musketon grant get name --me <wif> --consumer <consumer public key> --license

```

After a feature is granted by the user, the consumer can read the granted feature by doing:

```
musketon consumer read name --me <consumer wif> --user <user public key>
```

To see the audit trail of the reads done by the consumer, run:

```
musketon audittrail --me <wif> --consumer <consumer public key or address>
```

To revoke the grant, run:

```
musketon grant revoke name --me <wif> --consumer <consumer public key or address>
```

## Development

`musketon` is a Java/JVM project, using [Gradle](https://gradle.org/) as the build tool. It is mostly written in [Xtend](http://www.eclipse.org/xtend/) and is supported by a couple of `neon-js` scripts for blockchain interaction. It uses [protobuf](https://developers.google.com/protocol-buffers/) for the client entities and [Bouncy Castle](https://www.bouncycastle.org/) for the cryptography.

The project consists of:

* the smart contract: subproject `contract`
* the Java client plus CLI: subproject `client`
* the protobuf entities used by the client: subproject `client-protobuf`
* a util package: subproject `neo-util`

To build, using the `gradlew`/`gradle.bat` included in the project root, run:

```
gradle build
```

To compile the contract's NEO bytecode `.avm` file with [neoj](https://github.com/neo-project/neo-compiler/tree/master/neoj), create a `local.properties` file in the project root containing the path to your `neoj.dll`:

```
neojPath=/path/to/your/neoj/bin/Release/netcoreapp1.1/neoj.dll
```

And then run:

```
gradle neoj
```

The `.avm` file will show up in the `contract/build/neoj` folder.

To create the `musketon` CLI `.tar` distribution, run:

```
gradle client:distTar
```

To start coding in Eclipse, install the Eclipse Xtend plugin from the Eclipse marketplace and run:

```
gradle generateProto eclipse
```

## Future plans

### Browser extension

Create a browser extension, similar to the ones that password manager apps provide, that uses the `musketon` client to invoke the authorize operation with a single click. Upon a third party website's request (possibly through the presence of a specific html tag with some metadata), the extension would bring up a confirmation prompt, listing the features that the website would like to access and the expiry time.

A website could present an second form that just has a single text field for the extension to fill in the public key, as demonstrated in the webshop example mock-up below:

<img src="https://raw.githubusercontent.com/musketon/musketon/master/docs/res/webshop.png" width=1024 />

Clicking the `musketon` extension icon would bring up the extension sheet:

<img src="https://raw.githubusercontent.com/musketon/musketon/master/docs/res/webshop-extension-overlay.png" width=1024 />

Clicking _Authorize_ would invoke the `musketon` client's `authorize` and fill in the public key after which the form could be submitted. The consumer then has the public key necessary to read out the granted data.

To take it one step further, webshop owners could even be completely ruled out of the private data exchange currently needed to fulfill a webshop order. Instead of the user authorizing the webshop, the webshop could forward the grant request to the shipping courier right away. The user would then authorize the shipping courier instead of the webshop. When shipping the package, the webshop (thus not knowing the user's indentity) would just put a NEO address on the package label instead of the sensitive private data. Only the shipping courier, at the end of the order fulfillment chain, would need to read out the data to actually deliver the package.

### .wallet file

Currently to authenticate in the CLI, a 'naked' WIF command line arg is needed for every invocation. It would be nicer to use a `neo-python`-generated `.wallet` file with a password prompt.

### Support more features

`musketon` currently only supports few basic definable features. Supporting more features is easy and does not require a new smart contract deployment, but only a new entry in the client's `FeatureSpec`. Future additions could be:

* email address
* phone number
* bank account
* gender
* dietary preferences
* passport number
* medical profile
* national identity number / SSN
* ...many more

### Support more licenses

Currently only the 'read' license is implemented. Future additions could be the 'copy' and 'expose' license.

### Peer reviews

* Have more NEO developers and cryptography connaisseurs look at the architecture and code
* Have legal professionals look at the licenses.

### More metadata and insights

The current `musketon` implementation focuses on the core commands. Accompanied with a desktop app or webapp, it would be nice to be able get more metadata: listing all grants, sorting consumers by last read invocation, seeing which consumers use your data the most, etc. 

### Popular repo distribution

Distribute `musketon` to popular repositories like Homebrew, Maven Central, etc.

## Deployment status

The `musketon` smart contract is currently deployed on the [CoZ TestNet](https://coz.neoscan-testnet.io/), with script hash: `15bdde3554c411e2427a1b7903460c9cdd6dec22`
