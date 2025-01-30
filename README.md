# Console Kit

Console Kit is an SDK for building autonomous DeFi agents while providing programmatic access to Console's core DeFi utilities. The SDK enables developers to create sophisticated agents that can manage user funds and execute complex strategies, all secured by Console's policy engine and execution infrastructure. Essential DeFi primitives like optimal swap routing, MEV-protected execution, and cross-chain liquidity management are exposed as modular functions, enabling flexible integration paths from simple utility use to full autonomous agents.

The SDK abstracts away the underlying complexity of sub-accounts, policy management, and transaction execution, allowing developers to focus on building powerful autonomous strategies while inheriting Console's security features.

## System Architecture & Core Concepts

The [System Architecture & Core Concepts documentation](./docs/introduction.md) provides a comprehensive overview of Console Kit's design principles, components, and terminology. This section is essential reading for developers to understand:

- Core architectural components and their interactions
- Key terminologies and concepts used throughout the SDK
- Security model and policy engine fundamentals
- Integration patterns and best practices

We recommend reviewing this documentation before starting development to ensure a solid foundation in Console Kit's principles.

## Installation

To install the SDK, use npm or yarn:

```sh
npm install brahma-console-kit
```

or

```sh
yarn add brahma-console-kit
```

## Getting Started with Template

To quickly bootstrap your Console Kit project, you can use our [scaffold agent repository](https://github.com/Brahma-fi/scaffold-agent)

The scaffold repository includes a collection of example implementations showcasing how to build autonomous DeFi agents using Console Kit. This repository demonstrates integration patterns ranging from LLM-powered execution to automated DeFi workflows.

## Overview

### ConsoleKit

[`ConsoleKit`](./src/kit.ts) is the main class that provides access to the core functionalities of the SDK. It requires an API key and a base URL for initialization.

**Example:**

```typescript
import ConsoleKit from "brahma-console-kit";

const apiKey = "your-api-key";
const baseURL = "https://api.consolekit.com";

const consoleKit = new ConsoleKit(apiKey, baseURL);
```

### CoreActions

[`CoreActions`](./src/helpers/CoreActions/index.ts) provides core DeFi functions such as sending tokens and swapping assets, as well as fetching user information.

**Example:**

```typescript
const coreActions = consoleKit.coreActions;

async function fetchAccounts(eoa: string) {
  const accounts = await coreActions.fetchExistingAccounts(eoa);
  console.log(accounts);
}
```

### PublicDeployer

[`PublicDeployer`](./src/helpers/PublicDeployer/index.ts) handles executor subscription and brahma account deployments directly through EOAs in a gasless manner.

**Example:**

```typescript
const publicDeployer = consoleKit.publicDeployer;

async function deployStrategy(
  owner: string,
  chainId: number,
  feeToken: string
) {
  const preComputeData = await publicDeployer.fetchPreComputeData(
    owner,
    chainId,
    feeToken
  );
  console.log(preComputeData);
}
```

### AutomationContext

[`AutomationContext`](./src/helpers/AutomationContext/index.ts) manages automation services, including subscribing to, updating, and canceling automated tasks.

**Example:**

```typescript
const automationContext = consoleKit.automationContext;

async function subscribeToAutomation(params: any) {
  const response = await automationContext.subscribeToAutomation(params);
  console.log(response);
}
```

This overview provides a basic understanding of how to initialize and use the main classes in the `ConsoleKit` SDK. For more detailed usage, refer to the documentation or explore the source code.

## License

This project is licensed under the MIT License.
