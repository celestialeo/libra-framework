# Twin

## Overview

The `twin` concept within the Libra Framework's rescue tools is designed to create a synchronized, cloned environment of the network. This cloned environment, or twin, is used for comprehensive testing and validation, ensuring that changes and new implementations can be safely tested against a network state identical to production.

## Why We Want It

The need for a twin environment arises from the necessity to conduct thorough testing and validation in a controlled yet realistic setting. By replicating the production network's state, developers and testers can:
- Validate new features and bug fixes.
- Test network behaviors under controlled conditions.
- Ensure the robustness and reliability of updates before deploying them to production.

## What Twin Does

The twin setup process involves:
1. **Cloning the Production Database**: Copy the production database to create a local test database.
2. **Configuring New Validators**: Set up a new set of validators and generate the necessary configuration files.
3. **Creating a Rescue Blob**: Generate a rescue blob with the provided validator credentials.
4. **Applying the Rescue Blob**: Apply the rescue blob to the cloned database and configure the twin network to mirror the production environment.
5. **Ensuring Network Health**: Ensure that the twin network is operational and healthy by performing liveness checks and connectivity tests.

### Key Functions and Their Roles

- **TwinOpts**: Defines the options for setting up the twin, including the database path and optional operator file.
- **Twin**: Holds the configuration for the twin network, including paths and flags.
- **TwinRunner**: Trait that defines the `run` method for executing the twin setup.
- **TwinSetup**: Trait with various async functions for initializing and configuring the twin environment.

#### Initialization and Configuration
- **initialize_marlon_the_val**: Sets up a new validator using a temporary swarm.
- **register_marlon_tx**: Creates a registration transaction for the validator.
- **make_rescue_twin_blob**: Generates a rescue blob with the provided validator credentials.
- **apply_with_rando_e2e**: Main function that:
  1. Sets up a new validator set.
  2. Replaces the swarm database with the cloned production database.
  3. Applies the rescue blob to the swarm database.
  4. Configures nodes with updated settings.
  5. Ensures the twin network is operational and healthy.

#### Maintenance and Operation
- **extract_credentials**: Extracts and returns validator credentials from a node.
- **clone_db**: Copies the production database to the test database.
- **wait_for_node**: Waits for nodes to reach a healthy and connected state.

## Why It Matters

The twin environment is crucial for ensuring the stability and reliability of the Libra network. By replicating the production environment, developers can identify and resolve issues in a safe setting, reducing the risk of disruptions in the live network. This leads to a more resilient and dependable network infrastructure.

## Steps to Create and Use Twin

### Step 1: Clone the Production Database

1. **Identify the Path**: Locate the path to the production database.
2. **Copy the Database**: Copy the production database to a local directory for the twin environment.

```rust
fn clone_db(prod_db: &Path, swarm_db: &Path) -> anyhow::Result<()> {
    // Copy production DB to swarm DB location
    // Ensure paths exist and perform the copy operation
}
```

### Step 2: Initialize Validators 

1. **Set Up Validators**: Use a temporary swarm to set up new validators.
2. **Generate Configurations**: Generate the necessary configuration files for the validators.

```rust
async fn initialize_marlon_the_val() -> anyhow::Result<PathBuf> {
    // Initialize a new validator and return the path to the operator.yaml file
}
``` 

### Step 3: Create Rescue Blob

1. **Generate the Rescue Blob**: Create a rescue blob with the provided validator credentials.
2. **Save the Blob**: Ensure the rescue blob is correctly formatted and saved. 

```rust
async fn make_rescue_twin_blob(
    db_path: &Path,
    creds: Vec<&ValCredentials>,
) -> anyhow::Result<PathBuf> {
    // Create rescue blob and save it
}
```

### Step 4: Apply Rescue Blob

1. **Replace Test Database**: Use the cloned production database.
2. **Apply Rescue Blob**: Apply the rescue blob to configure the twin network.
3. **Update Configurations**: Update node configurations with new settings.
4. **Restart Nodes**: Restart the nodes to apply the changes.

```rust
async fn apply_with_rando_e2e(
    prod_db: PathBuf,
    num_validators: u8,
) -> anyhow::Result<LibraSmoke, anyhow::Error> {
    // Apply rescue blob and update configurations
}
```

### Step 5: Ensure Network Health

1. **Perform Liveness Checks**: Ensure all nodes in the twin network are operational.
2. **Conduct Connectivity Tests**: Confirm nodes can communicate effectively.
3. **Monitor and Resolve Issues**: Monitor the network for any issues and resolve them as necessary.

```rust
async fn wait_for_node(
    validator: &mut dyn Validator,
    expected_to_connect: usize,
) -> anyhow::Result<()> {
    // Wait for nodes to be healthy and connected
}
```

By following these steps, you can create a twin network environment that mirrors the production network, allowing for thorough testing and validation in a controlled setting.

