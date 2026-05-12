# CyberRangeCZ Platform Demo Training

Linear game for [CyberRangeCZ Platform](https://docs.platform.cyberrange.cz/).

Follow [general instructions](https://docs.platform.cyberrange.cz/basic-concepts/typical-training-workflow/training-workflow-cloud/) to set up the game.

This branch is prepared for Azure-backed sandbox provisioning.

## Game Levels Summary
- `nmap` port scanning
- `hydra` password guessing at `telnet`
- privilege escalation using misconfigured `sudo`

## Topology summary
|Host|Image|Flavor|
|-|-|-|
|client|Canonical:0001-com-ubuntu-server-jammy:22_04-lts-gen2:latest|Standard_B4ms|

The telnet target runs as the `server` Docker container on the `client` VM.
The APG-generated `telnet_port`, `alice_flag`, and `root_flag` values are
applied during Ansible provisioning.
Current sandbox-service Docker support still creates the automatic MAN VM, so
Azure-backed deployments use two VMs total: MAN plus `client`.

## License and Credits
[MIT License](./LICENSE)

**Leading author:** Zdeněk Vydra

**Contributors:** Jakub Čegan, Tomáš Sapák, Kamil Andoniadis, Igor Ignác, Juraj Paluba, Dominik Pilár, Michal Urban, Tomáš Kacvinský
