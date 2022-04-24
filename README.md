# Running Node.js in an Azure Function

## Goals

### Deploy the funciton with a GitHub Actions workflow

```
func azure functionapp publish <name_of_func_app>
```

### Track progress of function

Monitor an ongoing function through another function. One endpoint may trigger a
long task, while another endpoint reports the progress made. Otherwise, let the
function use web sockets to have an interrupt-like tracking of the progress and
not polling.

### Singleton function

Make only one instance of a function possible at the same time, such that
multiple long tasks can not be started.

## Notes

### HttpTrigger

The `authLevel` property determines what keys, if any, need to be present on the request in order to invoke the function.

* **anonymous**: No API key is required
* **function**: (default) A function-specific API key is required. Does not change between deployments and can be renewed.
* **admin**: The master key is required

See [the documentation](https://docs.microsoft.com/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger.authlevel?view=azure-java-stable) for further details.