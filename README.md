# Forge Chronicles

The Forge Chronicles library is a tool that generates a json file and a human readable markdown log file with the deployment information about contracts deployed using `forge script`. It can keep track of upgrades for transparent proxies and generates a history of deployments. An example for such a log can be found [here](https://github.com/0xPolygon/pol-token/blob/main/deployments/5.md). Logs are generated by extracting information from the `run-latest.json` file generated by `forge script` in the `broadcast` directory.

## Requirements

The script utilizes Node.js to run. We recommend the node version defined in the `.nvmrc` file.

## Installation

```bash
forge install 0xPolygon/forge-chronicles
```

## Usage Example

The following command will create a log for the contracts deployed in the `Deploy.s.sol` script on Ethereum mainnet.

```bash
node lib/forge-chronicles Deploy.s.sol --chain-id 1 --rpc-url https://mainnet.infura.io/v3/{your-infura-key}
```

## Usage

The deployment markdown & json log file will be placed within the `deployments` directory. The name of the file will be the chain id of the network where the script was executed (e.g., for Ethereum mainnet the files will be `deployments/1.md` and `deployments/json/1.json`).

Supplying the RPC url _can_ be optional. When contracts are deployed, the RPC url is used to check whether the deployed contracts implement a `version()` function. If they do, the version is extracted and recorded within the log file. If no RPC url is supplied, the version check is skipped.

Supplying the RPC url is _required_ when an upgrade is deployed for a transparent proxy. The script can recognize when an upgrade is deployed, however, most of the times, only an implementation is deployed and the actual upgrade is performed by a multisig or governance. When an upgrade is detected, the RPC url will be used to verify that the upgrade was performed on chain directly and only then, deployment log files will be generated. If the upgrade was not performed on chain yet, the script will abort.

## Flags

| --flag          | -flag | Description                                                                |
| --------------- | ----- | -------------------------------------------------------------------------- |
| --chain-id      | -c    | Chain id of the network where the script was executed (default: 31337)     |
| --rpc-url       | -r    | RPC url used for versioning and upgrade verification (default: $RPC_URL)   |
| --explorer-url  | -e    | Explorer url to use for links in markdown (default: blockscan)             |
| --skip-json     | -s    | Skip generation of json file and only generate markdown from existing json |
| --broadcast-dir | -b    | Directory where the broadcast files are stored (default: broadcast)        |
| --out-dir       | -o    | Directory where the foundry output files are stored (default: out)         |
| --force         | -f    | Force the generation of the json file with the same commit                 |
| Options         |       |                                                                            |
| --help          | -h    | Print help                                                                 |
| --version       | -v    | Print the version number                                                   |

## License

​
Licensed under either of
​

- Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)
  ​

at your option.

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.

---

© 2023 PT Services DMCC
