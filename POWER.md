---
name: "launchdarkly"
displayName: "LaunchDarkly"
description: "Manage feature flags, environments, and AI configurations directly from your IDE using LaunchDarkly's official MCP server. Create, update, and evaluate flags with natural language commands."
keywords: ["launchdarkly", "feature flags", "toggles", "experiments", "rollouts", "targeting"]
author: "LaunchDarkly"
---

# LaunchDarkly

## Overview

The LaunchDarkly power enables you to manage feature flags, environments, and AI configurations directly from your IDE using natural language commands. Built on LaunchDarkly's official MCP server, this power lets you create, update, evaluate, and manage feature flags without leaving your development environment.

Key capabilities include:
- **Feature Flag Management**: Create, read, update, delete, and archive feature flags
- **Environment Control**: Manage flag states across different environments (development, staging, production)
- **Targeting Rules**: Set up user targeting, percentage rollouts, and complex flag logic
- **AI Configuration Management**: Handle AI-specific configurations and settings
- **Code References**: Track where flags are used in your codebase
- **Natural Language Interface**: Use conversational commands instead of complex API calls

This power is perfect for developers who want to integrate feature flag management into their development workflow, enabling faster iteration and safer deployments.

## Onboarding

### Prerequisites

Before using this power, ensure you have:
- **LaunchDarkly Account**: Sign up for a free account at [launchdarkly.com](https://app.launchdarkly.com/signup?utm_source=kiro&utm_medium=referral)
- **JavaScript Runtime**: Node.js with ECMAScript 2020 or newer support
- **API Access Token**: A LaunchDarkly API token with appropriate permissions

### Creating a LaunchDarkly API Access Token

1. **Navigate to Authorization Settings**:
   - Click the gear icon in LaunchDarkly's left sidebar
   - Select "Authorization"

2. **Create New Access Token**:
   - In the "Access tokens" section, click "Create token"
   - Give your token a descriptive name (e.g., "Kiro MCP Server")
   - Assign a role - "Writer" role is recommended for full functionality

3. **Save Your Token**:
   - Click "Save token"
   - **Important**: Copy and securely store the token immediately
   - The token will be obscured after you leave the page

### Recommended Token Permissions

For full MCP server functionality, create a custom role with these permissions:

```json
[
  {
    "effect": "allow",
    "actions": ["*"],
    "resources": ["proj/${roleAttribute/projectKey}:env/*:flag/*"]
  },
  {
    "effect": "allow",
    "actions": ["*"],
    "resources": ["proj/${roleAttribute/projectKey}:env/*:aiconfig/*"]
  },
  {
    "effect": "allow",
    "actions": ["viewProject"],
    "resources": ["proj/${roleAttribute/projectKey}"]
  }
]
```

### Installation

The LaunchDarkly MCP server is automatically configured when you install this power. No additional installation steps are required.

## Common Workflows

### Workflow 1: Creating Feature Flags

**Goal**: Create new feature flags for your application features

**Natural Language Commands**:
```
Create a feature flag called "new-checkout-flow" in my project
```

**Steps**:
1. The MCP server will prompt for your project key if not specified
2. Provide your project name or key when requested
3. Click "Run tool" to execute the flag creation
4. Verify the flag appears in your LaunchDarkly dashboard

**Example Conversation**:
```
You: "Create a feature flag called 'awesome-new-feature' in my raccoon-api-facts project"
Agent: I'll create the feature flag for you.
[Click "Run tool" to execute]
Result: Feature flag 'awesome-new-feature' created successfully
```

### Workflow 2: Managing Flag States

**Goal**: Turn flags on/off across different environments

**Natural Language Commands**:
```
Turn the "new-checkout-flow" flag ON in all environments
Turn off the "experimental-ui" flag in production only
Enable "dark-mode" flag in development environment
```

**Steps**:
1. Specify the flag name and desired state
2. Optionally specify target environments
3. Click "Run tool" to apply changes
4. Verify changes in LaunchDarkly dashboard

**Example**:
```
You: "Turn the 'awesome-new-feature' flag ON in all environments"
Agent: I'll enable the flag across all environments.
[Click "Run tool" to execute]
Result: Flag enabled in Test and Production environments
```

### Workflow 3: Setting Up Targeting Rules

**Goal**: Create sophisticated targeting rules for gradual rollouts

**Natural Language Commands**:
```
Update targeting for "new-feature" so it's only enabled for users in Canada
Add a targeting rule for "beta-feature" for users whose email ends in @company.com
Set up a 25% rollout for "performance-improvement" flag
```

**Steps**:
1. Describe your targeting criteria in natural language
2. The MCP server will translate this into proper targeting rules
3. Click "Run tool" to apply the targeting configuration
4. Test the targeting with different user contexts

**Example**:
```
You: "Update targeting rules for 'awesome-new-feature' so it's only enabled for users in Canada"
Agent: I'll create a targeting rule for Canadian users.
[Click "Run tool" to execute]
Result: Targeting rule created for country = "CA"
```

### Workflow 4: Evaluating Flags

**Goal**: Test how flags will behave for different users

**Natural Language Commands**:
```
Evaluate "new-checkout-flow" for user with email john@company.com
Check what "premium-features" returns for a user in the US
Test "experimental-ui" flag for user ID 12345
```

**Steps**:
1. Specify the flag and user context
2. The agent will run the evaluation logic
3. Review the returned flag value and reasoning
4. Adjust targeting rules if needed

**Example**:
```
You: "Evaluate 'awesome-new-feature' for user with email test@launchdarkly.com"
Agent: For user test@launchdarkly.com, the flag returns: true
Reason: User matches targeting rule for @launchdarkly.com emails
```

### Workflow 5: Flag Lifecycle Management

**Goal**: Manage flags through their complete lifecycle

**Natural Language Commands**:
```
List all feature flags in my project
Show me details about the "checkout-redesign" flag
Archive the "old-feature" flag
Delete the "temporary-test" flag
Copy the configuration from "feature-a" to create "feature-b"
```

**Steps**:
1. Use descriptive commands for the action you want
2. Specify flag names and any additional parameters
3. Click "Run tool" for each operation
4. Confirm changes in LaunchDarkly dashboard

## Troubleshooting

### MCP Server Connection Issues

**Problem**: MCP server won't start or connect
**Symptoms**:
- Error: "Connection refused"
- Server not responding
- Tools not appearing in IDE

**Solutions**:
1. **Verify Installation**: Ensure the MCP server package is accessible
   ```bash
   npx -y @launchdarkly/mcp-server
   ```

2. **Check API Token**: Verify your API token is correct and has proper permissions
   - Token should start with `api-`
   - Check token permissions in LaunchDarkly Authorization settings

3. **Environment Variables**: If using environment variables, ensure they're properly set
   ```bash
   echo $MCP_LD_TOKEN  # Should display your token
   ```

4. **Restart IDE**: Restart your AI client/IDE after configuration changes

### Authentication Errors

**Error**: "Unauthorized" or "Invalid API token"
**Cause**: API token issues
**Solutions**:
1. Verify token is correctly copied (no extra spaces)
2. Check token hasn't expired
3. Ensure token has required permissions for the operation
4. For EU/Federal instances, verify correct server URL is configured

### Tool Execution Errors

**Error**: "Project not found" or "Flag not found"
**Cause**: Incorrect project/flag names or insufficient permissions
**Solutions**:
1. **Verify Project Key**: Use exact project key from LaunchDarkly dashboard
2. **Check Flag Names**: Ensure flag keys match exactly (case-sensitive)
3. **Permissions**: Verify API token has access to the specified project
4. **Environment**: Confirm you're targeting the correct LaunchDarkly environment

### Rate Limiting

**Error**: "Rate limit exceeded"
**Cause**: Too many API requests in short time period
**Solutions**:
1. Wait a few minutes before retrying
2. Batch operations when possible
3. Consider using fewer concurrent operations

### Environment-Specific Issues

**Problem**: Wrong LaunchDarkly instance (EU/Federal vs Commercial)
**Symptoms**: Connection works but wrong data appears
**Solutions**:
1. **EU Customers**: Add `--server-url https://app.eu.launchdarkly.com` to configuration
2. **Federal Customers**: Add `--server-url https://app.launchdarkly.us` to configuration
3. Update mcp.json configuration and restart IDE

## Best Practices

- **Use Descriptive Flag Names**: Choose clear, meaningful names for your feature flags
- **Specify Project Context**: Always mention your project name to avoid confusion
- **Test Targeting Rules**: Use flag evaluation to verify targeting works as expected
- **Environment Awareness**: Be explicit about which environments you're targeting
- **Regular Cleanup**: Archive or delete unused flags to keep your project organized
- **Gradual Rollouts**: Use percentage targeting for safer feature releases
- **Monitor Changes**: Verify changes in LaunchDarkly dashboard after MCP operations

## When to Load Steering Files

### `launchdarkly-flag-cleanup.md` - LaunchDarkly feature flag cleanup workflow

Steering workflow that uses the LaunchDarkly MCP server to safely automate feature flag cleanup workflows. This workflow determines LaunchDarkly feature flag removal readiness, identifies the correct forward value, and creates PRs that preserve production behavior while removing obsolete flags and updating stale defaults.

## Configuration

### Basic Configuration

**No additional configuration required** - the power works immediately after installation with your API token.

### Advanced Configuration Options

**Restrict Tool Access**: Limit which MCP tools are available by adding specific tools to the configuration:

```json
{
  "mcpServers": {
    "LaunchDarkly": {
      "command": "npx",
      "args": [
        "-y", "--package", "@launchdarkly/mcp-server", "--", "mcp", "start",
        "--tool", "create-feature-flag", 
        "--tool", "update-feature-flag",
        "--api-key", "your-api-key-here"
      ]
    }
  }
}
```

**Environment-Specific Configuration**: For EU or Federal LaunchDarkly instances:

```json
{
  "mcpServers": {
    "LaunchDarkly": {
      "command": "npx",
      "args": [
        "-y", "--package", "@launchdarkly/mcp-server", "--", "mcp", "start",
        "--api-key", "your-api-key-here",
        "--server-url", "https://app.eu.launchdarkly.com"
      ]
    }
  }
}
```

## MCP Config Placeholders

**IMPORTANT**: Before using this power, replace the following placeholder in `mcp.json` with your actual values:

- **`api-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`**: Your LaunchDarkly API access token.
  - **How to get it**:
    1. Go to LaunchDarkly dashboard → Organization settings → Authorization
    2. Click "Create token" in the Access tokens section
    3. Give it a name and assign "Writer" role for full functionality
    4. Click "Save token" and copy the generated token
    5. Replace the placeholder with your actual token (starts with `api-`)

**After replacing the placeholder, your mcp.json should look like:**
```json
{
  "mcpServers": {
    "LaunchDarkly": {
      "command": "npx",
      "args": [
        "-y", "--package", "@launchdarkly/mcp-server", "--", "mcp", "start",
        "--api-key", "api-your-actual-token-here"
      ]
    }
  }
}
```

---

This power integrates with LaunchDarkly MCP Server (MIT license)

**Package**: `@launchdarkly/mcp-server`
**MCP Server**: LaunchDarkly