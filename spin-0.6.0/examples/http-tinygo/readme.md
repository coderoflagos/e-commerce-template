# Spin HTTP components in (Tiny)Go

This example showcases how to build Spin HTTP components using TinyGo.

```go
package main

import (
	"fmt"
	"net/http"

	spinhttp "github.com/fermyon/spin/sdk/go/http"
)

func init() {
	spinhttp.Handle(func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type", "text/plain")
		fmt.Fprintln(w, "Hello Fermyon!")
	})
}

func main() {}
```

> For more information and examples for using TinyGo with WebAssembly, check
> [the official TinyGo documentation](https://tinygo.org/docs/guides/webassembly/)
> and
> [the Wasm examples](https://github.com/tinygo-org/tinygo/tree/release/src/examples/wasm).

Building this as a WebAssembly module can be done using the `tinygo` compiler:

```shell
$ make build
tinygo build -wasm-abi=generic -target=wasi -no-debug -o main.wasm main.go
```

Finally, we can create a Spin application configuration to execute this
component:

```toml
apiVersion = "0.1.0"
authors = ["Fermyon Engineering <engineering@fermyon.com>"]
description = "A simple Spin application written in (Tiny)Go."
name = "spin-hello-world"
trigger = { type = "http", base = "/" }
version = "1.0.0"

[[component]]
id = "hello"
source = "main.wasm"
[component.trigger]
route = "/hello"
```

At this point, we can execute the application with the `spin` CLI:

```shell
$ make serve
RUST_LOG=spin=trace spin up --file spin.toml
```

The application can now receive requests on `http://localhost:3000/hello`:

```shell
$ curl -i localhost:3000/hello
HTTP/1.1 200 OK
content-type: text/plain; charset=utf-8
content-length: 16
date: Wed, 09 Mar 2022 17:23:08 GMT

Hello, Fermyon!
```
