# Keeping your validator up to date

## References
- [Solana Validator Educational Workshop: Software Updates And Restarts](https://www.youtube.com/watch?v=HKR5dn5CSZo&list=PLilwLeBwGuK6jKrmn7KOkxRxS9tvbRa5p&index=4)
- [Solana Docs: Operation Best Practices](https://docs.solanalabs.com/operations/best-practices/general)

## Key Take aways
1. Keep an eye on announcements in the Discord channels:
- [testnet announcements](https://discord.com/channels/428295358100013066/594138785558691840)
- [mainnet-beta announcements](https://discord.com/channels/428295358100013066/669406841830244375)
2. Remember, you are managing system infrastructure. No shortcuts!
3. Avoid restarting when deliquency is > 5%.
4. Minimize downtime by:
- Installing the Solana update prior to restart.
- Bundle server updates together for fewer restarts.

## Quick Reference
### Make sure you are on the correct server.
Seems simple but it's easy to get confused. Just double check.

### Check your leader schedule
Keep enough time for restart AND catchup. To be extra safe target a window big enough for some troubleshooting.

[MAS DeFi Leader Schedule Tool](https://masdefi.vercel.app/leaderSchedule)


### Install new version

This will install the new version, extract, and initialize the new version while the validator is running.
```
solana-install init <version>
```
Restart your validator when there is enough time to restart and catchup between leader slots. Exit auto triggers shutdown and the auto restart is handled by the systemd service.
```
solana-validator --ledger /mnt/ledger/ exit --max-delinquent-stake 5 --min-idle-time 30
```
You will see it saving a new snapshot
```
⠒ 00:00:10 | Processed Slot: 272322562 | Full Snapshot Slot: 272313893 | Incremental Snapshot Slot: 272322440 | 0.67% delinquent stake | Waiting for a new snapshot    
```

To monitor catchup(Note: It may take a couple minutes to work. Check the status using other methods in the meantime to ensure the validator restarted succesfully.)
```
solana catchup yourValidatorID
```
You're done when catchup displays
```
 ... has caught up (us:27232xxxx them:27232xxxx)
 ```
 

### Helpful trouble shooting commands. Customize to your setup.
```
grep -B1 'Starting validator with' solana-validator.log
sudo journalctl -u sol.service -n 200
systemctl
systemctl status sol.service 
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
