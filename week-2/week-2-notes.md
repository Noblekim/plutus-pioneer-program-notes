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

-- Display the type.
:t I 42

-- Activate the OverloadedStrings extension.
:set -XOverloadedStrings -- Convert 'String' literals to other types, such as the 'ByteString' type.

B "Haskell" -- ByteString

-- Construct a 'Map'.
Map [(I 32, B "Haskell"), (List [I 0], I 1000)]
```

### Gift Module

The module Gift, in the Gift.hs file, allows users to send ada to a script address and anyone can redeem those ada.

The code is commented to explain what it does.

#### Playground

The playground shows the two endpoints under "Available functions".

### Burn Module

The validator can result in an error by changing the validator to:

```hs
mkValidator _ _ _ = error ()
```

The 'error' function is not from the standard Haskell prelude. 'PlutusTx.Prelude' overrides the standard prelude. The GHC extension 'NoImplicitPrelude' stops the standard prelude from being loaded.

Since the validator always ends in an error, ada sent to the script address are inaccessible.

### FortyTwo Module

The script validates only if the redeemer is 42.

The 'ToData' class has a method 'toBuiltinData' that converts a type to 'BuiltinData'.
The 'FromData' class does the opposite.

REPL

```hs
import PlutusTx
import PlutusTx.IsData.Class

toData () -- Constr 0 []
fromData (Constr 0 []) :: Maybe () -- Just ()

toData (42 :: Int) -- I 42
fromData (I 42) :: Maybe Integer -- Just 42
```

The unstable 'MakeIsData' does not guarantee which constructor is used. The stable version requires an explicit definition of which constructor to use.

### Homework

The scripts should validate if the two Booleans in the validator are the same.
