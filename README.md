# Solana Validator Startup Notes

Notes from getting a validator running on test net. Start with the excellent Solana Guides 
- [Setup a Solana Validator
](https://docs.solanalabs.com/operations/setup-a-validator)
- [Solana Validator Educational Workshop Series](https://www.youtube.com/playlist?list=PLilwLeBwGuK6jKrmn7KOkxRxS9tvbRa5p)

Time stamp links here are to video [Getting Started as a Validator Part 1](https://youtu.be/b0-vMyoojuo?si=ZqyjOej1lpmk4nhN)

## Overall Tips
1. Treat TestNet like the real thing.
2. Take your time. Understand what the commands are really doing.

## Solana CLI
Use the --help command. It is truly helpful. It enables you to explore and understand the interface.
```
solana --help
solana balance --help
```
With less you can search the help section.
```
solana --help | less
```
There is a good conversation about server operations install here: [47:37](https://youtu.be/b0-vMyoojuo?si=q6yjKH3_nfp8qDyr&t=2857)


## Create Keys
DO NOT use the same keys on TestNet and MainNet.

Good Conversation here: [6:25](https://youtu.be/b0-vMyoojuo?si=ZqyjOej1lpmk4nhN&t=385)

Note: If you're targeting the Solana Delegation program the keys you sign up with are you're keys for the duration of the program. So keep them safe! And, if you want vanity ID keys create them now.

## SSH Into your Validator
[Solana Validator Education - SSH Setup + sol User](https://youtu.be/nYoZOkpiMmk?si=iXHF-rKAbI4nWcVP)

[Solana Validator Security Best Practices](https://docs.solanalabs.com/operations/best-practices/security#do-not-store-your-withdrawer-key-on-your-validator)

## Hard Drive Setup
Ensure your drives are mounted after restarts! You will fill up your main drive quickly if you start the validator without the drives mounted.

Good converstation here: [50:03](https://youtu.be/b0-vMyoojuo?si=qT7xLJmYDo5CKp-U&t=3003)

## Moving Key Pairs
Only move the keypairs that you need. Remember wallets don't hold tokens, it's all on the chain. So you can access information about wallets on the server from you local computer.
[45:59](https://youtu.be/b0-vMyoojuo?si=POfMEJFK4fzFTE2P&t=2759)

## Validator Startup Script
Be sure script files contain #!/bin/bash or the system services won't run them. [1:00:15](https://youtu.be/b0-vMyoojuo?si=pD95W32jhPG-cumI&t=3615)

## Verify the Validator is Working
It is really cool when you see the logs running :) Congrats.

Check for start log
```
grep -B1 'Starting validator with' solana-validator.log 
```
Note: How to Stop Validator: [Part 2 - 36:53](https://youtu.be/nY2SFjaDXHw?si=_MFZD04w7xPQ9JWz&t=2160)
### A Note on Staking

If you have no acive stake yet you need to an extra flag.
```
solana validators -ut --keep-unstaked-delinquents | grep <pubkey>
```
More info on staking: [Solana Staking Doc](https://docs.solanalabs.com/operations/guides/validator-stake)

Note: If you see an error like 
```
Error: Dynamic program error: No default signer found, run "solana-keygen new -o /home/sol/.config/solana/id.json" to create a new one
```
You can create a new Idenity or more likely you need to specify the identity you already created. It's trying to use the CLI config. So set the default your validator-keypair.json or specify the signer.


## Create a System Service
Check for validator process
```
ps aux | grep solana-validator
```
Check active system services
```
systemctl list-units --type=service --state=running | grep sol.serv
```


## Monitoring
Video: [Solana Validator Education - Monitoring and Metrics](https://youtu.be/lLxC0BXC08k?si=FGyJhG7HRqx8PuDs)
- Setup on another server
- Setup notifications for server issues


