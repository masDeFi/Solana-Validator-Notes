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


This will install the new version, extract, and initialize the new version while the validator is running.
```
solana-install init <version>
```
Restart your validator when there is enough time to restart and catchup between leader slots. Exit auto triggers shutdown and the auto restart is handled by the systemd service.
```
solana-validator --ledger /mnt/ledger/ exit --max-delinquent-stake 5 --min-idle-time 30
```

To monitor catchup
```
solana catchup yourValidatorID
```
Helpful trouble shooting commands. Customize to your setup.
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

## Protocol
1. Double check the version to install
2. Install
```
solana init <version>
```
3. Restart with System Service configured to auto start
```
solana-validator --ledger /mnt/ledger/ exit --max-delinquent-stake 5 --min-idle-time 5
```
will see output like this![wait-for-restart output](image.png)
4. Confirm restart. Check version, service and catchup
```
grep -B1 'Starting validator with' <path/to/logfile>


Output:
[2024-04-28T14:45:49.223542765Z INFO  solana_validator] solana-validator 1.18.12 (src:b9c13825; feat:4215500110, client:SolanaLabs)
[2024-04-28T14:45:49.223575785Z INFO  solana_validator] Starting validator with: ArgsOs {
```
```
service sol status
```
![Sol service status output](image-2.png)

```
solana catchup <validatorID>
```
![Solana Catcup output](image-1.png)
...CiPEEVwaVexyB has caught up (us:267400896 them:267400906)