# Artifacts

The hard fork requires certain artifacts. All those artifacts can be reproduced by anyone (not only validator participants).

## Framework Source
The Move framework binariescan be produced with this command from
```
# assumes branch release-7.0.0
cd libra-framework
libra move framework release
```
## Migration list
To produce a JSON file with a snapshot of the V6 chain with all accounts (no exclusions), follow this:
```
# assumes branch release-7.0.0
cd libra-framework/storage
cargo run export-snapshot -m ~/libra-framework/tools/storage/fixtures/state_epoch_79_ver_33217173.795d/state.manifest
```

## Drop list
A list of accounts to drop can be produced by following the steps here: https://github.com/0LNetworkCommunity/scorpions-claws
