# Rust RPC client for Blackcoin More JSON-RPC 

This is a Rust RPC client library for calling the Blackcoin More JSON-RPC API. It provides a layer of abstraction over 
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Blackcoin JSON-RPC interface 

This git package compiles into two crates.
1. [blackcoinmore-rpc](https://crates.io/crates/blackcoinmore-rpc) - contains an implementation of an rpc client that exposes 
the Blackcoin More JSON-RPC APIs as rust functions.

2. [blackcoinmore-rpc-json](https://crates.io/crates/blackcoinmore-rpc-json) -  contains rust data structures that represent 
the json responses from the Blackcoin More JSON-RPC APIs. blackcoinmore-rpc depends on this.

# Usage
Given below is an example of how to connect to the Blackcoin More JSON-RPC for a Blackcoin More node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `15715` and the node
is set up to accept RPC connections. 

```rust
extern crate blackcoinmore_rpc;

use blackcoinmore_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:15715",
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples. 

# Supported Blackcoin More Versions
The following versions are officially supported and automatically tested:
* 25.1.0

# Minimum Supported Rust Version (MSRV)
This library should always compile with any combination of features on **Rust 1.48.0**.
