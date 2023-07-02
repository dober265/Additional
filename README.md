cascadiad keys show wallet -a
journalctl -u cascadiad -f -o cat
sudo systemctl restart cascadiad
curl localhost:26657/status
curl -s localhost:26657/status | jq .result.sync_info.catching_up
cascadiad keys show wallet --bech val -a
cascadiad tx staking delegate YOUR_VALOPER_ADDRESS 1000000aCC --from wallet --chain-id $CHAIN_ID --fees 5000aCC
cascadiad query staking validators --limit 2000 -o json | jq -r '.validators[] | select(.status=="BOND_STATUS_BONDED") | [.operator_address, .status, (.tokens|tonumber / pow(10; 6)), .description.moniker] | @csv' | column -t -s"," | sort -k3 -n -r
cascadiad query staking validators --limit 2000 -o json | jq -r '.validators[] | select(.status=="BOND_STATUS_UNBONDED") | [.operator_address, .status, (.tokens|tonumber / pow(10; 6)), .description.moniker] | @csv' | column -t -s"," | sort -k3 -n -r
#ports
26656, 26657, 9091, 9090, 6060, 1317
