# Start Nodes
# 9. Create or Download artifacts
To create artifacts [go here: create_artifacts.md](create_artifacts.md)

## direct download:

V6 Epoch 79 Snapshot [(link)](artifacts/state_epoch_79_ver_33217173.795d.json
)

```
wget https://raw.githubusercontent.com/0LNetworkCommunity/v7-hard-fork-ceremony/main/artifacts/state_epoch_79_ver_33217173.795d.json -P $HOME/.libra/
```

Scorpion's Claw Drop List: [(link)](artifacts/drop_list.json)
```
wget https://raw.githubusercontent.com/0LNetworkCommunity/v7-hard-fork-ceremony/main/artifacts/drop_list.json -P $HOME/.libra/
```

# 10. Build Genesis TX
```
libra genesis build -o 0o-de-lally -n a-genesis -l -j $HOME/.libra/state_epoch_79_ver_33217173.795d.json --drop-list $HOME/.libra/drop_list.json
```

# 11. Start node

```
libra node
```
