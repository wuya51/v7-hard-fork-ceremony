# Start Nodes

# 9. Build Genesis TX
```
libra genesis build -o 0o-de-lally -n a-genesis -l -j ~/libra-framework/tools/genesis/tests/fixtures/sample_export_recovery.json --drop-list ~/libra-framework/tools/genesis/tests/fixtures/drop.json.full
```

If you would like to reproduce this list from the original migration file, with `--drop-file drop.json`

# 9. Start node

```
libra node
```
