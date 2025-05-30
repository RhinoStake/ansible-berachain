# Ansible Playbook for Berachain Node Initialization and Management

[![ansible-lint](https://github.com/RhinoStake/ansible-berachain/actions/workflows/ansible-lint.yml/badge.svg?branch=main)](https://github.com/RhinoStake/ansible-berachain/actions/workflows/ansible-lint.yml)

Ansible playbook for Berachain Validators and RPCs delivered to bare metal servers. This playbook is intended for node runners who utilize bare metal servers,
delivering both Beacond and Reth, Geth or Nethermind via Docker.

## This repo features:

- Ability to initialize an Berachain node (validator, rpc) via docker containers, including initing the node, configuring beacond, and running container with
  proper port management.
- Ability to run reth, geth or nethermind as an execution layer engine. Set `execution_client` in the appropriate vars file as well as included the appropriate
  execution version.
- Ability to upgrade to a new versions when requested for planned upgrades.
- This playbook does not include core server setup, security, monitoring, or power management components necessary for server security and performance. These
  components are the responsibility of the operator.
- Assumes docker is installed and all appropriate firewall rules are in place (docker ports will bypass ufw)
- Utilizes Berachain team provided beacond config files & modifies only necessary components. Therefore if additional chain configurations or tweaks are
  utilized, re-running these playbooks will add/modify those configurations.
- This repo is entirely impotent and can be re-run indefinitely.

## How to setup this repository

1. Copy inventory file

   `cp inventory.sample inventory.ini`

   Update information in the inventory file. Mostly like you will need to update the server IP and hostname fields, create groups, all that.

2. Review the group_vars values for each network, modify Fee Recipient Address

## How to use this repository

- Set `execution_client` in the appropriate var file (mainnet, testnet). This will default to `reth` if not set.
- Update `run_node` to add additional port ACLs if the requirement for off-node RPC calls exists.
- Init'ing a new node: `ansible-playbook berachain_mainnet.yaml --limit nodename-in-inventory`. The nodes are filtered via inventory groups.

- Upgrading to a new version as provided by Berachain. Update the `consensus_version` in the appropriate var file and re-run the playbook.
- Upgrading to a new execution version. Update the `execution_version` in the appropriate var file and re-run the playbook.

Have ideas/changes/additions? Great! Feel free to push a PR to this repo or reach out to [me on Discord](https://discord.gg/SGhQzj5tyz)!

## Boost the RHINO!

If this repository has been helpful, consider
[boosting our validator](https://hub.berachain.com/validators/0x93012bdcf6baa87c1737df03c5fac7c8bb447282fbca5d2de42726ec67f237d66a2f867853e32ebd295010f075f22e95/)!

## Who is RHINO?

RHINO is a professionally managed, highly available validator service. Earn rewards and help secure networks by staking your tokens with RHINO. We operate
across the Berachain, Aptos, Cosmos, Chainlink, and Sei ecosystems. Read more at [https://rhinostake.com](https://rhinostake.com). We build trust into every
block.

We additionally provide Berachain RPC & Snapshot services at [https://berachain-apis.com](https://berachain-apis.com) - get started!
