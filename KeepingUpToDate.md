# Keeping your validator up to date

## References
- [Solana Validator Educational Workshop: Software Updates And Restarts](https://www.youtube.com/watch?v=HKR5dn5CSZo&list=PLilwLeBwGuK6jKrmn7KOkxRxS9tvbRa5p&index=4)

## Key Take aways
1. Keep an eye on announcements in the Discord channels:
- [testnet announcements](https://discord.com/channels/428295358100013066/594138785558691840)
- [mainnet-beta announcements](https://discord.com/channels/428295358100013066/669406841830244375)
2. Remember, you are managing system infrastructure. No shortcuts!
3. Avoid restarting when deliquency is > 5%.
3. Minimize downtime by:
- Installing the Solana update prior to restart.
- Bundle server updates together for fewer restarts.

## Quick Reference
```
solana-install <version>
```
```
solana-validator --ledger /mnt/ledger/ wait-for-restart-window --max-delinquent-stake 5 --min-idle-time 30
```
```
solana catchup yourValidatorID
```


## Diving Deeper
#### Restart Windows
It is important that validators don't stop producing blocks while the leader.
- Won't produce blocks
- Skip rate will increase
- Overall network performance will decrease

Use the **wait-for-restart-window** becuase it takes that into account. 
```
solana-validator wait-for-restart-window
vs
solana-validator exit
```
[7:36](https://youtu.be/HKR5dn5CSZo?si=D9fltFzvEWffFU9P&t=456)\
Note: You must have systemd setup to auto restart