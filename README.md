## Build the Rust library

```
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
$ cd rust
$ rustup override set nightly
$ cargo build --release
```


## Test Go code

```
$ cd go
$ cp ../rust/target/release/librustposeidongold.a .
$ go test
```

## Benchmark Go code

```
$ cd go
$ go test -bench .
```

Example output on a system with AMD Ryzen 9 7950X CPU:
```
goos: linux
goarch: amd64
pkg: github.com/okx/poseidongold/go
cpu: AMD Ryzen 9 7950X 16-Core Processor
BenchmarkRustWrapper-32                  1359136               865.9 ns/op
BenchmarkVectorizedPoseidonGold-32        775248              1517 ns/op
PASS
```

## Build for Alpine Linux

This is needed to build [xlayer-erigon](https://github.com/okx/xlayer-erigon).

```
$ docker run -v .:/poseidon -it docker.io/library/golang:1.22-alpine3.20 sh
# *** in the container:
# apk add curl
# apk add build-base
# cd /poseidon/rust
# curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
# . "$HOME/.cargo/env"
# rustup override set nightly
# cargo build --release
# cp target/release/librustposeidongold.a ../go/
# cd ../go
# go test
```

## License

Apache License, Version 2.0 [LICENSE](LICENSE)