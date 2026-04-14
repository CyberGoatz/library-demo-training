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
|server|Canonical:0001-com-ubuntu-server-noble:24_04-lts:latest|Standard_B2s|
|client|Canonical:0001-com-ubuntu-server-noble:24_04-lts:latest|Standard_B2s|
|router|Canonical:0001-com-ubuntu-server-noble:24_04-lts:latest|Standard_B2s|

## License and Credits
[MIT License](./LICENSE)

**Leading author:** Zdeněk Vydra

**Contributors:** Jakub Čegan, Tomáš Sapák, Kamil Andoniadis, Igor Ignác, Juraj Paluba, Dominik Pilár, Michal Urban, Tomáš Kacvinský
