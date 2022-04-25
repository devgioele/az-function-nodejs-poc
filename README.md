# Running Node.js in an Azure Function

## Goals

### Deploy the function with a GitHub Actions workflow

### Track function progress

Monitor an ongoing function through another function. One endpoint may trigger a
long task, while another endpoint reports the progress made. Otherwise, let the
function use web sockets to have an interrupt-like tracking of the progress and
not polling.

### Singleton function

Make only one instance of a function possible at the same time, such that
multiple long tasks can not be started.

## Notes

### Settings to test Azure Functions locally

In the root directory, add a `local.settings.json` file with the following
content.

```json
{
  "IsEncrypted": false,
  "Values": {
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "AzureWebJobsStorage": ""
  }
}
```

This is a basic settings file to get started. Secrets may be added in the 
future, which is why this file is not pushed to the repo.

### Authorization

The `authLevel` property of a function determines what keys, if any, need to be present on the
request in order to invoke the function.

- **anonymous**: No API key is required
- **function**: (default) A function-specific API key is required. Does not
  change between deployments and can be renewed.
- **admin**: The master key is required

See
[the documentation](https://docs.microsoft.com/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger.authlevel?view=azure-java-stable)
for further details.

### Durable Functions

Durable Functions are stateful functions that make [singletons](https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-singletons?tabs=javascript) possible.

To use them, install the extension:
`yarn add durable-functions`

However, web sockets are not supported, meaning that monitoring can only take place in a polling-like manner.