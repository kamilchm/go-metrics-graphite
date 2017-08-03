This is a reporter for the [go-metrics](https://github.com/rcrowley/go-metrics)
library which will post the metrics to Graphite.
It was originally part of the `go-metrics` library itself, but has been split off to
`github.com/cyberdelia/go-metrics-graphite` and then forked here.

`cyberdelia`'s version needs a resolved `net.TCPAddr` which makes it fragile
in dynamic environments, where Graphite address can points to distributed
cluster where specific hosts can change. Starting your app with `cyberdelia`
version means that you can loose its metrics when one of Graphite hosts in cluster
will be replaced.

This fork provides an interface with address provided as a `string`.
You can provide a DNS name to it and it will resolve metrics target
before each flush operation, so you can swap Graphite hosts and
send app metrics to new location without restarting it.

### Usage

```go
import "github.com/kamilchm/go-metrics-graphite"


go graphite.Graphite(metrics.DefaultRegistry,
  1*time.Second, "some.prefix", "graphite-cluster:2003")
```
