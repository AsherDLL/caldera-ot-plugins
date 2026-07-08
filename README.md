# Caldera OT Protocol Plugins

A set of protocol plugins for [MITRE Caldera](https://github.com/mitre/caldera) that
are not part of the official [caldera-ot](https://github.com/mitre/caldera-ot)
collection. Each plugin adds adversary-emulation abilities for one OT protocol, mapped
to [ATT&CK for ICS](https://attack.mitre.org/matrices/ics/), and driven by a small
command-line client that runs on a Caldera agent.

Every plugin ships a GUI panel, an output parser, a sample fact source, unit tests,
and cross-platform build workflows. Each one was tested end to end against a live
protocol server and had its on-the-wire traffic verified.

## Plugins

| Protocol | Repository | License | Abilities | Related to |
|---|---|---|---|---|
| IEC 60870-5-104 | [caldera-iec104](https://github.com/AsherDLL/caldera-iec104) | GPL-3.0 | 6 | Industroyer, CosmicEnergy |
| Siemens S7 (S7comm) | [caldera-s7comm](https://github.com/AsherDLL/caldera-s7comm) | Apache-2.0 | 6 | Stuxnet |
| OPC-UA | [caldera-opcua](https://github.com/AsherDLL/caldera-opcua) | Apache-2.0 | 5 | PIPEDREAM |
| M-Bus (Meter-Bus) | [caldera-mbus](https://github.com/AsherDLL/caldera-mbus) | Apache-2.0 | 5 | Fuxnet |

A separate repository,
[ot-protocol-validation](https://github.com/AsherDLL/ot-protocol-validation), holds the
harness used to verify the traffic each plugin generates.

## Status against the official caldera-ot

MITRE's caldera-ot currently ships six plugins: modbus, dnp3, bacnet, iec61850,
profinet, and gems. None of the four protocols in this collection are in it yet.

| Protocol | In mitre/caldera-ot |
|---|---|
| IEC-104 | No |
| S7comm | No |
| OPC-UA | No |
| M-Bus | No |

## Install

Each plugin is a standard Caldera plugin. Clone it into your Caldera `plugins/`
directory and enable it in `conf/local.yml`. For example, for S7comm:

```
git clone https://github.com/AsherDLL/caldera-s7comm plugins/s7comm
```

```yaml
plugins:
  - s7comm
```

Restart Caldera. The abilities appear under their ATT&CK for ICS tactics, and a sample
fact source is available to seed a target. Payload binaries ship in each plugin's
`payloads/` directory, with Windows and macOS binaries produced by the release
workflow.

## Testing

Each plugin was validated with the
[ot-protocol-validation](https://github.com/AsherDLL/ot-protocol-validation) harness,
which starts a capture, runs the payload, and asserts that the expected protocol
message is on the wire. The harness supports both TCP and UDP protocols and keeps the
captures so they can be opened in Wireshark.

## Responsible use

These are offensive tools for real OT protocols. Use them only on systems you own or
have written authorization to test. Some abilities stop safety controllers or disrupt
a running process. Run them in a lab, not on production equipment.

## License

This umbrella repository is Apache-2.0. Each plugin keeps its own license, shown in the
table above. caldera-iec104 is GPL-3.0 because it bundles the GPL-licensed c104
library; the others are Apache-2.0.
