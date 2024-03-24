# PIT Phase 2 repo project: Cross-chain Proof of NFT

This repository is created to enter the PIT phase 2.

## Team Members

- @binhtam456

## Description

This application enables a user to submit a vote a ballot on a contract on OP Sepolia. The information about this vote subsequently gets sent to an ERC721 NFT contract on Base Sepolia to mint an NFT related to the vote.

Features:

- Uses Polymer x IBC as the cross-chain format
- Commits to the spirit of application specific chains/rollups where voting functionality could be specialized on one chain, NFT marketplace on another and both can form composable applications through interoperability.

## Resources used

The repo uses the [ibc-app-solidity-template](https://github.com/open-ibc/ibc-app-solidity-template) as starting point and adds custom contracts XBallot and XProofOfVoteNFT that implement the custom logic.

It changes the send-packet.js script slightly to adjust to the custom logic.

The expected behaviour from the template should still work but nevertheless we quickly review the steps for the user to test the application...
Run `just --list` for a full overview of the just commands.

Additional resources used:
- Hardhat
- Blockscout
- Tenderly

## Steps to reproduce

After cloning the repo, install dependencies:

```sh
just install
```

And add your private key to the .env file (rename it from .env.example).

### Sending a packet

Now with an existing channel in the config (your own or the default), run:

```sh
just do-it
```
You'll see an active waiting poll in the terminal and will be informed if the packet was sent successfully.

## Proof of testnet interaction

After following the steps above you should have interacted with the testnet. You can check this at the [IBC Explorer](https://sepolia.polymer.zone/packets).

Here's the data of our application:

- XBallot (OP Sepolia) : 0x21bCf2cAf9494aBD7dab28C2E376CD560eF1FF0d
- XProofOfVoteNFT (Base Sepolia): 0xe801b0ea5d98677a4a408d4252b9c6c4bcb3cb8a
- Channel (OP Sepolia): channel-39296
- Channel (Base Sepolia): channel-39297

- Proof of Testnet interaction:
    - [SendTx](https://optimism-sepolia.blockscout.com/tx/0x24cd9569275ce19b94df5c53787800aa911e5135c8e4fc7e7816ee76c95e7031)
    - [RecvTx](https://base-sepolia.blockscout.com/tx/0xf8f658b04985718a2f140f7cd3d23da2e5007c7a2ba763b9e654db74f8195dfe)
    - [Ack](https://optimism-sepolia.blockscout.com/tx/0xcf65f93e93bc90d571b4cf298a034672b3f5b960bccdce1deb5d9021346aa53b)

## Challenges Faced

- Debugging used to be tricky when the sendPacket on the contract was successfully submitted but there was an error further down the packet lifecycle.
What helped was to verify the contracts and use Tenderly for step-by-step debugging to see what the relayers submitted to the dispatcher etc.

## What we learned

How to make the first dApp using Polymer.

## Future improvements

Basic functionality was implemented, but the following things can be improved:

- More tests
- More input validation
- Add event listeners related to important IBC lifecycle steps

## Licence

[Apache 2.0](LICENSE)
