#  Ceremony Registration

Note: to confirm correctness of the artifacts here, please [follow these instructions, in create_artifacts.md](create_artifacts.md)

##  Version 7 Hard Fork Upgrade

# 1. Get github token

Go to github.com
developer settings >
personal access tokens (classic) >
create token (classic) >
check only one box:
"public_repo"

Put it in this file:

`echo <THE TOKEN> $HOME/github_token.txt`

NOTE: You may later paste this into the `libra register` command later.

<img width="75%" alt="Screenshot 2024-04-09 at 12 36 25 PM" src="https://github.com/0LNetworkCommunity/v7-hard-fork-ceremony/assets/1364012/43ef28fe-af81-412a-9509-cb125dbf5f9d">


# 2. Make your box
```
cd ~
rm -fr ~/libra-framework
git clone https://github.com/0LNetworkCommunity/libra-framework
cd ~/libra-framework
git fetch --all
git checkout release-7.0.0
git log -n 1 --pretty=format:"%H"

```

# 3. Install Dependencies

```
cd ~/libra-framework/util
bash dev_setup.sh

```

# 4. Wipe Libra home

We want to make sure you have a clean slate (in case you've used this box before).


```
rm -rf ~/.libra
```

# 5. Build the source


```
cd ~/libra-framework
cargo build --release -p libra
cp target/release/libra ~/.cargo/bin
which libra
```

# 6. Register

copy command verbatim, do not change the org name to your own.
Your ~/.libra folder will be created now. And the github_token.txt file will be checked, and copied there.

```
libra genesis register --org-github 0o-de-lally --name-github a-genesis --token-github-file $HOME/github_token.txt
```

Q: Do you need to register for genesis? 
A:  Yes

# 7. Port Check
You will run a script so that the coordinator can check that your node can connect to peers, and that your firewall is set up correctly

```
cd ~/libra-framework
bash ./util/port_check.sh
```

# 8. Wait

Everyone needs to register, and the Genesis Coordinator needs to prepare some files after that.

Build Genesis
```
libra genesis build -o 0o-de-lally -n a-genesis -l -j ~/libra-framework/tools/genesis/tests/fixtures/sample_export_recovery.json --drop-list ~/libra-framework/tools/genesis/tests/fixtures/drop.json.full
```

If you would like to reproduce this list from the original migration file, with `--drop-file drop.json`

# 9. Start node

```
libra node
```



## Helpers

### What are the firewall recommendations?:

```
cd ~/libra-framework
bash ./util/default_firewall.sh

```


### Who is connected to my validator?

```
netstat -n | grep 6180 | grep ESTABLISHED

```

# Ceremony Policies:
- Registration has firm cutoff time, PRs will stop being accepted
- Nodes that fail the port check will be excluded
- A first genesis will be attempted with all qualifying nodes
- If that launch fails to get consensus:
  - The N Testnet Validators will form the base, and N/2 New Registrants will join
  - If there are more New Registrants than N/2:
    - The N/2 New Registrants will be prioritized based on prior registration on an 0L Network
    - If still more than N/2 then it will be in order of registration time on GitHub
- If it fails again:
  - just take the nodes that successfully connected in the prior step


