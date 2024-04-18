# SolanaValidatorStatupNotes

These are notes from getting a validator running on test net. The intent is to provide extra information and useful tips related to the startup guide. First, start with the excellent Solana Guides 
- [Setup a Solana Validator
](https://docs.solanalabs.com/operations/setup-a-validator)
- [Solana Validator Educational Workshop Series](https://www.youtube.com/playlist?list=PLilwLeBwGuK6jKrmn7KOkxRxS9tvbRa5p)

Time stamp links here are to video [Getting Started as a Validator Part 1](https://youtu.be/b0-vMyoojuo?si=ZqyjOej1lpmk4nhN)

## Overall Tips
1. Treat TestNet like the real thing.
2. Take your time. Understand what commands are really doing.
3. Take notes for later reference

## Solana CLI
Use the --help command. It is truly helpful. It enables you to explore and understand the interface.
```
solana --help
solana balance --help
```
Using less allows you to search the help section which can save time.
```
solana --help | less
```
There is a good conversation about server operations install here: [47:37](https://youtu.be/b0-vMyoojuo?si=q6yjKH3_nfp8qDyr&t=2857)


## Create Keys
DO NOT use the same keys on TestNet and MainNet
Good Conversation here: [6:25](https://youtu.be/b0-vMyoojuo?si=ZqyjOej1lpmk4nhN&t=385)

## Hard Drive Setup
Ensure your drives are mounted after restarts! You will fill up your main drive quickly if you start the validator without the drives mounted.

Good converstation here: [50:03](https://youtu.be/b0-vMyoojuo?si=qT7xLJmYDo5CKp-U&t=3003)
