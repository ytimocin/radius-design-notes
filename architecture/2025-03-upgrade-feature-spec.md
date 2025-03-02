# Topic: Radius Control Plane Upgrades

- **Author**: Yetkin Timocin (@YetkinTimocin)

## Topic Summary

The Radius control plane upgrades feature aims to streamline the process of upgrading the control plane components of the Radius platform. This includes ensuring compatibility with new versions, minimizing downtime, and providing a seamless upgrade experience for users. The feature will draw on best practices from similar projects such as Dapr, Crossplane, and Istio.

### Top level goals

- Ensure a smooth and reliable upgrade process for the Radius control plane.
- Minimize downtime and disruption during upgrades.
- Provide clear documentation and guidance for users performing upgrades.

### Non-goals (out of scope)

- Upgrading user data and application components.
- Introducing new features unrelated to the upgrade process.

## User profile and challenges

The primary users of this feature are system administrators and DevOps engineers responsible for maintaining and upgrading the Radius platform.

### User persona(s)

- **System Administrator**: Responsible for managing the infrastructure and ensuring the smooth operation of the Radius platform.
- **DevOps Engineer**: Focused on automating deployment processes and maintaining the CI/CD pipeline.

### Challenge(s) faced by the user

- Ensuring compatibility with new versions of the control plane components.
- Minimizing downtime and disruption during the upgrade process.
- Navigating complex upgrade procedures without clear documentation.

### Positive user outcome

Users will be able to upgrade the Radius control plane with minimal downtime and disruption, ensuring compatibility with new versions and maintaining the stability of their systems.

## Key scenarios

### Scenario 1: Upgrading the control plane using the Radius CLI

Users can upgrade the control plane components using the Radius CLI, following a series of commands to ensure a smooth upgrade process.

### Scenario 2: Upgrading the control plane using Helm

Users can upgrade the control plane components using Helm, leveraging Helm charts to manage the upgrade process.

### Scenario 3: Upgrading the control plane in a Kubernetes environment

Users can upgrade the control plane components in a Kubernetes environment, following best practices for Kubernetes upgrades.

## Key dependencies and risks

- **Dependency Name**: Radius CLI – The upgrade process relies on the Radius CLI for executing upgrade commands. Issues/concerns/risks: Compatibility with new versions of the CLI.
- **Dependency Name**: Helm – The upgrade process relies on Helm for managing the upgrade process. Issues/concerns/risks: Compatibility with new versions of Helm.
- **Dependency Name**: Contour – The upgrade process relies on Contour for routing requests. Issues/concerns/risks: Compatibility with new versions of Contour.
- **Risk Name**: Downtime during upgrades – Mitigation plan: Implement rolling upgrades and provide clear documentation to minimize downtime.

## Key assumptions to test and questions to answer

- Assumption: Users have the necessary permissions and access to perform upgrades.
- Question: What are the common issues users face during the upgrade process, and how can we address them?
- Plan: Conduct user research and gather feedback to identify common issues and improve the upgrade process.

## Current state

The current state of the Radius control plane upgrade process involves manual steps and limited documentation. Users have reported challenges with compatibility and downtime during upgrades.

## Details of user problem

As a system administrator, I need to upgrade the Radius control plane components to ensure compatibility with new versions and maintain the stability of my systems. However, the current upgrade process is complex and prone to errors, leading to downtime and disruption.

## Desired user experience outcome

After this scenario is implemented, I can upgrade the Radius control plane components seamlessly, with minimal downtime and disruption. As a result, my systems remain stable and compatible with new versions.

### Detailed user experience

1. User initiates the upgrade process using the Radius CLI or Helm.
2. The system performs pre-upgrade checks to ensure compatibility.
3. The upgrade process is executed, with rolling upgrades to minimize downtime.
4. The system performs post-upgrade checks to verify the success of the upgrade.
5. User receives a notification confirming the successful upgrade.

## Key investments

### Feature 1

Implement pre-upgrade and post-upgrade checks to ensure compatibility and verify the success of the upgrade.

### Feature 2

Provide clear documentation and guidance for users performing upgrades using the Radius CLI and Helm.

### Feature 3

Implement rolling upgrades to minimize downtime and disruption during the upgrade process.

### Database Upgrade Process

The Radius database upgrade process involves migrating the data store from etcd to a PostgreSQL database. This change aims to improve service continuity and decouple state management from etcd. Here are the key steps involved in the upgrade process:

1. **Preparation**: Before starting the upgrade, ensure that PostgreSQL is deployed to the Kubernetes cluster. This can be done using the Helm chart for installing Radius, which now includes deploying PostgreSQL.
2. **Migration**: The data from etcd is migrated to the PostgreSQL database. This involves exporting the existing data from etcd and importing it into PostgreSQL. The migration process ensures that all necessary data is transferred accurately.
3. **Configuration**: Update the Radius configuration to point to the new PostgreSQL database. This includes updating connection strings and any other relevant settings to ensure that Radius can communicate with the PostgreSQL database.
4. **Verification**: After the migration and configuration updates, perform thorough testing to verify that the upgrade was successful. This includes checking that all data is accessible and that the system is functioning as expected.
5. **Monitoring**: Monitor the system closely after the upgrade to ensure that there are no issues. This includes checking logs, performance metrics, and any other relevant indicators to ensure that the system is stable.

### Dry-Run Upgrade Process

Implementing a dry-run option for the Radius control plane upgrades will allow users to simulate the upgrade process without making any actual changes. This helps in identifying potential issues and ensuring a smooth upgrade when executed for real. The dry-run process will include the following steps:

1. **Initiate Dry-Run**: User initiates the dry-run process using the command `rad upgrade --dry-run`.
2. **Simulate Upgrade**: The system simulates the upgrade process, performing all the steps without making any actual changes.
3. **Generate Report**: The system generates a report detailing the steps that would be taken during the actual upgrade, including any potential issues or conflicts.
4. **Review Report**: User reviews the report to identify and address any potential issues before proceeding with the actual upgrade.

### Plan for `rad upgrade`

The `rad upgrade` command will be designed to facilitate the upgrade process for the Radius control plane components. Here is the plan for implementing the `rad upgrade` command:

1. **Command Structure**: The `rad upgrade` command will follow a similar structure to the `rad install kubernetes` command, with additional options for performing upgrades.
2. **Pre-Upgrade Checks**: The command will perform pre-upgrade checks to ensure compatibility with the existing configuration and identify any potential issues.
3. **Dry-Run Option**: The command will include a `--dry-run` option to simulate the upgrade process without making any actual changes. This will help users identify potential issues before performing the actual upgrade.
4. **Upgrade Execution**: The command will execute the upgrade process, including updating the control plane components, applying any necessary database migrations, and updating configurations.
5. **Post-Upgrade Checks**: The command will perform post-upgrade checks to verify the success of the upgrade and ensure that the system is functioning as expected.
6. **Rollback Option**: The command will include a rollback option to revert to the previous version in case of any issues during the upgrade process.

By following this plan, the `rad upgrade` command will provide a reliable and user-friendly way to upgrade the Radius control plane components, ensuring compatibility with new versions and minimizing downtime and disruption.
