# QnA

## Run scripts on testnet?

It is possible to run scripts on the testnet, but the transactions will have to be handcrafted.

## Datum vs Redeemer?

Datum sits with the output, the person who locks the funds. Redeemer comes from the person who wants to use the UTxO as an input. Redeemer is a key that unlocks the transaction.

## When to use Untyped?

The size of a script is limited and using Untyped decreases the size as compared to Typed.

## How to understand the code better?

Use the language server.

## Is there tooling to view code on the blockchain?

Not yet, as most code is open source. The source code can be compiled and hashed to verify.

## Why is the hash of the validator required?

It is not for the previous examples, but it used to be in previous versions.

## Possible to retrieve all redeemers at once?

No, only the redeemer of the current input can be viewed.

## Where is the Datum stored?

It is stored in the transactions. If only the hash is provided, then the UTxO cannot be consumed.
