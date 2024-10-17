# How to Run a Fuel Testnet Node

This guide provides step-by-step instructions on how to set up and run a Fuel testnet node. This will allow you to interact with the Fuel network, participate in its ecosystem, and help improve its decentralization.

## Prerequisites

Before you begin, ensure you have the following:

1. **System Requirements**:
   - A computer with at least 4 GB of RAM.
   - A modern multi-core CPU.
   - At least 10 GB of free disk space (SSD recommended for better performance).
   - A stable internet connection.

2. **Software Dependencies**:
   - **Rust**: Install Rust by following the instructions on the [official Rust website](https://www.rust-lang.org/tools/install).
   - **Cargo**: This is usually installed alongside Rust.
   - **Docker**: If you want to use Docker for running the node, install Docker from [Docker's official website](https://www.docker.com/get-started).

## Step 1: Install the Fuel Node

### Clone the Repository

Start by cloning the Fuel node repository from GitHub:

```bash
git clone https://github.com/fuel-network/fuel-core.git
cd fuel-core
```

### Build the Node

Next, build the node using Cargo:

```bash
cargo build --release
```

This command compiles the code into an optimized binary, which will be located in the `target/release` directory.

## Step 2: Configure the Node

### Create a Configuration File

Create a configuration file for your node. You can use the provided example or customize it to your preferences. Here’s how to create a simple configuration file:

```bash
mkdir config
touch config/testnet.yaml
```

Open `testnet.yaml` in a text editor and add the following content:

```yaml
network:
  name: "testnet"
  port: 3030
  rpc_port: 8545
```

### Modify Ports

Ensure that the ports specified in your configuration file are open and not being used by other applications.

## Step 3: Run the Node

### Start the Node

You can now run your node with the following command:

```bash
./target/release/fuel-core --config config/testnet.yaml
```

This command starts your Fuel testnet node, which will begin syncing with the network.

### Running with Docker (Optional)

If you prefer to use Docker, you can run the node with the following command:

```bash
docker run -it --rm fuel/fuel-core:latest --config /path/to/config/testnet.yaml
```

Replace `/path/to/config/testnet.yaml` with the path to your configuration file.

## Step 4: Verify Node Synchronization

To check if your node is running properly and syncing with the network, monitor the logs:

```bash
tail -f target/release/logs/debug.log
```

You should see logs indicating that your node is connecting to peers and syncing blocks.

## Step 5: Interact with the Node

Once your node is running and synchronized, you can interact with it via JSON-RPC. You can use tools like `curl` or Postman to send requests to the RPC endpoint specified in your configuration.

### Example RPC Request

Here's an example of how to get the node's status:

```bash
curl -X POST http://localhost:8545 \
-H "Content-Type: application/json" \
-d '{"jsonrpc": "2.0", "id": 1, "method": "eth_blockNumber", "params": []}'
```

This request retrieves the current block number from your node.

## Troubleshooting

### Common Issues

1. **Node Not Syncing**: Ensure that your internet connection is stable and the ports specified are open. Check the logs for any error messages.

2. **Performance Issues**: If the node is slow, consider allocating more resources (CPU/RAM) or using an SSD for better performance.

3. **Docker Issues**: Ensure Docker is installed correctly and that you have permissions to run Docker commands.
