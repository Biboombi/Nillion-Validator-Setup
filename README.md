# Nillion Validator Node Setup Guide

## Introduction

This repository provides a comprehensive guide for setting up a Nillion Validator Node. Nillion is a decentralized modular protocol designed to enhance liquidity on orderbook-based exchanges. Follow the instructions below to install and configure your Nillion validator node.

## Prerequisites

- **Operating System:** Ubuntu 22.04 (Windows and macOS users should refer to the official documentation)
- **Docker:** Ensure Docker is installed on your system.
- **Keplr Wallet:** For managing Nillion tokens and addresses.
- **Nillion Testnet Tokens:** Obtain these from the Nillion faucet.

## Installation and Setup

1. **Create a Wallet and Add Nillion Chain**

   - **Create a Wallet:**
     - Use [Keplr Wallet](https://www.keplr.app/) to create a wallet.
     - Add the Nillion test network to your wallet.

   - **Get Testnet Tokens:**
     - Go to [Nillion Faucet](https://faucet.testnet.nillion.com/) to obtain testnet tokens.

2. **Install Docker**

   - **Install Docker:**
     ```bash
     curl -fsSL https://get.docker.com | bash -s docker
     ```

   - **Verify Docker Installation:**
     ```bash
     docker --version
     docker container run --rm hello-world
     ```

3. **Set Up the Validator Node**

   - **Pull the Docker Image:**
     ```bash
     docker pull nillion/retailtoken-accuser:v1.0.0
     ```

   - **Create a Local Directory:**
     ```bash
     mkdir -p nillion/accuser
     ```

   - **Initialize the Validator Node:**
     ```bash
     docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
     ```

   - **Check Your Credentials:**
     ```bash
     vim ~/nillion/accuser/credentials.json
     ```

     - Use `:q` to exit `vim` after noting your Nillion address, public key, and private key.

   - **Import Your Wallet:**
     - Import the private key into Keplr Wallet.

4. **Register the Validator**

   - **Register as a Validator:**
     - Go to [Nillion Verifier Registration](https://verifier.nillion.com/verifier) to register using the generated address and public key.

5. **Start the Node**

   - **Start the Validator Node:**
     ```bash
     docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start [starting_block_height]
     ```

     - Replace `[starting_block_height]` with the starting block height from the web page.

   - **Check Sync Status:**
     ```bash
     curl -s https://testnet-nillion-rpc.lavenderfive.com/status | jq .result.sync_info
     ```

     - Ensure it shows `false` for a successful sync.

6. **Backup and Monitor**

   - **Backup Important Files:**
     ```bash
     cp ~/nillion/accuser/credentials.json ~/nillion/accuser/credentials_backup.json
     ```

   - **Run in Screen:**
     ```bash
     screen -S nillion
     docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start [starting_block_height]
     ```

     - Detach with `Ctrl+A+D` and reattach with `screen -r nillion`.

## Additional Resources

- [Nillion Official Guide](https://mirror.xyz/exploring.eth/Hb8M-w2oxGfaVTjXQcUmC2URn-ubcJPT6xYpmFYd0yc)
- [Nillion Testnet Faucet](https://faucet.testnet.nillion.com/)

## Contact

For further assistance, you can reach out on the [Nillion Discord](https://discord.gg/nillion) or follow updates on [Nillion Twitter](https://twitter.com/nillion).
