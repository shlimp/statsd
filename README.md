## Introduction

This is a fork of the statsd client from [alexcesaro](https://github.com/alexcesaro/statsd)
this fork is for use inside google app engine classic environment only

for the full documentation of the client go to https://godoc.org/gopkg.in/alexcesaro/statsd.v2

## Changes from the original package

Google App Engine doesn't let you use the built-in socket package, you have to use it's [custom package](https://cloud.google.com/appengine/docs/standard/go/sockets/reference)
the main difference in the packages is that Google Appp Engine package needs a context, which the regular package doesn't.
it's important to notice that for the package to work properly, the default FlushPeriod is 0, and should stay like that. if you will increase this value you will get inaccurate results
in order to keep this package as efficient as possible, a new client should be created only once in the warmup or start script with a context, and the on each stat a context needs to be passed.

### example
warmup:
```
ctx := appengine.NewContext(r)
statsd_client, statsd_err = statsd.New(statsd.Context(ctx))
```
request:
```
ctx := appengine.NewContext(r)
statsd_client.Gauge(ctx, 'gauge_name', 3)
```


## Documentation

https://godoc.org/gopkg.in/alexcesaro/statsd.v2


## Download

    go get https://github.com/shlimp/statsd


## Example

See the [examples in the documentation](https://godoc.org/gopkg.in/alexcesaro/statsd.v2#example-package).


## License

[MIT](LICENSE)
