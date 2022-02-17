# Week 2

## Triggering Change

Transactions on the blockchain are externally triggered. The transactions are passive. In the example of the auction, if the 'close' action is not invoked, then the token and ada are locked indefinitely.

## Low Level, Untyped Validation Scripts

### Sides of a Smart Contract

There are two sides to a smart contact: the on-chain part and the off-chain part.

The on-chain part validates transactions allows them to consume EUTxOs.

The off-chain part constructs and submits transactions.

### EUTxO Data

The EUTxO model extends the UTxO model by adding script address that can run logic. A validator node will run the script and decide whether the transaction is valid.

Plutus receives three pieces of data:

* The datum.
* The redeemer.
* The context.

Each use the same data type, but it can be customized at a computational cost.

### PlutusTx Module

The 'BuiltinData' data type is the type that is used in on-chain code.

The 'Data' data type is used in off-chain code and can be converted to 'BuiltInData'. It is similar to the JSON data type as it can represent arbitrary pieces of data.

REPL

```hs
import PlutusTx

-- Ask for information about the 'Data' type.
:i Data

-- Define values of the 'Data' type.
I 42 -- Integer

-- Display the type
:t I 42

-- Activate the OverloadedStrings extension.
:set -XOverloadedStrings -- Convert 'String' literals to other types, such as the 'ByteString' type.

B "Haskell" -- ByteString

-- Construct a 'Map'.
Map [(I 32, B "Haskell"), (List [I 0], I 1000)]
```
