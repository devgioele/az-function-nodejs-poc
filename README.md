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
