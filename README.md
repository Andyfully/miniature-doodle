Skip to content

Code
Issues
30
provides metadata for chains

chainid.network
License
 MIT license
 7.3k stars
 5.7k forks
 471 watching
 329 Branches
 7 Tags
 Activity
 Custom properties
Public repository
ethereum-lists/chains
Folders and files
Name	
Latest commit
ligi
ligi
5 minutes ago
History
.ci
4 years ago
.github
5 minutes ago
_data
9 minutes ago
gradle/wrapper
10 months ago
httpsloader
last year
model
6 months ago
processor
2 months ago
tools
10 months ago
website @ cb5b575
3 months ago
.gitignore
9 months ago
Repository files navigation
README
MIT license
EVM-based Chains
The source data is in _data/chains. Each chain has its own file with the filename being the CAIP-2 representation as name and .json as extension.

Example
{
  "name": "Ethereum Mainnet",
  "chain": "ETH",
  "rpc": [
    "https://mainnet.infura.io/v3/${INFURA_API_KEY}",
    "https://api.mycryptoapi.com/eth"
  ],
  "faucets": [],
  "nativeCurrency": {
    "name": "Ether",
    "symbol": "ETH",
    "decimals": 18
  },
  "features": [{ "name": "EIP155" }, { "name": "EIP1559" }],
  "infoURL": "https://ethereum.org",
  "shortName": "eth",
  "chainId": 1,
  "networkId": 1,
  "icon": "ethereum",
  "explorers": [{
    "name": "etherscan",
    "url": "https://etherscan.io",
    "icon": "etherscan",
    "standard": "EIP3091"
  }]
}
when an icon is used in either the network or an explorer there must be a json in _data/icons with the name used (e.g. in the above example there must be a ethereum.json and a etherscan.json in there) - the icon jsons look like this:

[
    {
      "url": "ipfs://QmdwQDr6vmBtXmK2TmknkEuZNoaDqTasFdZdu3DRw8b2wt",
      "width": 1000,
      "height": 1628,
      "format": "png"
    }
]
where:

the URL must be an IPFS url that is publicly resolvable
width and height are positive integers
format is either "png", "jpg" or "svg"
If the chain is an L2 or a shard of another chain you can link it to the parent chain like this:

{
  ...
  "parent": {
   "type" : "L2",
   "chain": "eip155-1",
   "bridges": [ {"url":"https://bridge.arbitrum.io"} ]
  }
}
where you need to specify type 2 and the reference to an existing parent. The field about bridges is optional.

You can add a status field e.g. to deprecate (via status deprecated) a chain (a chain should never be deleted as this would open the door to replay attacks) Other options for status are active (default) or incubating

Aggregation
There are also aggregated json files with all chains automatically assembled:

https://chainid.network/chains.json
https://chainid.network/chains_mini.json (miniaturized - fewer fields for smaller filesize)
Constraints
the shortName and name MUST be unique - see e.g. EIP-3770 on why
if referencing a parent chain - the chain MUST exist in the repo
if using a IPFS CID for the icon - the CID MUST be retrievable via ipfs get - not only through some gateway (means please do not use pinata for now)
for more constraints you can look into the CI
Collision management
We cannot allow more than one chain with the same chainID - this would open the door to replay attacks. The first pull request gets the chainID assigned. When creating a chain we can expect that you read EIP155 which states this repo. All pull requests trying to replace a chainID because they think their chain is better than the other will be closed. The only way to get a chain reassigned is when the old chain gets deprecated. This can e.g. be used for testnets that are short-lived. But then you will get the redFlag "reusedChaiID" that should be displayed in clients to warn them about the dangers here.

Getting your PR merged
before PR is submited
Before submitting a PR, please verify that checks pass with:

$ ./gradlew run

BUILD SUCCESSFUL in 7s
9 actionable tasks: 9 executed
Once PR is submitted
Make sure CI is green. There will likely be no review when the CI is red.
When making changes that fix the CI problems - please re-request a review - otherwise it is too much work to track such changes with so many PRs daily
Usages
Wallets
WallETH
TREZOR
Minerva Wallet
Explorers
Otterscan
EIPs
EIP-155
EIP-3014
EIP-3770
EIP-4527
Listing sites
chainid.network / chainlist.wtf
chainlist.org
networks.vercel.app
eth-chains
EVM-BOX
chaindirectory.xyz
chain-list.org
chainlist.network
evmchainlist.org
evmchainlist.com
thechainlist.io
chainlist.info
chainmap.io
chainlist.in
chainz.me
Chainlink docs
Wagmi compatible chain configurations
evmchain.info
Other
FaucETH

Sourcify playground

Smart Contract UI

Your project - contact us to add it here!

Releases
 7 tags
Packages
No packages published
Contributors
951
@ligi
@pedrouid
@dependabot[bot]
@solidityx
@3eph1r0th
@Thegaram
@FrederikBolding
@RareData
@ilovers
@benbaley
@bmann
@dfenstermaker
@ashutoshpw
@boundless-forest
+ 937 contributors
Deployments
500+
 github-pages 3 minutes ago
+ more deployments
Languages
Kotlin
94.1%
 
JavaScript
5.9%
Footer
© 2024 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact
Manage cookies
Do not share my personal information
Andyfully/miniature-doodle: echo "# Andyfully-" >> README.md git init git add README.md git commit -m "first commit" git branch -M main git remote add origin https://github.com/Andyfully/Andyfully-.git git push -u origin main
