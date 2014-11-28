rust-rocksdb
============

### running
- Cargo.toml
```rust
[dependencies.rocksdb]
git = "https://github.com/spacejam/rust-rocksdb"
```
- Code
```rust
extern crate rocksdb;

fn main() {
  match rocksdb::create_or_open("/path/for/rocksdb/storage".to_string()) {
    Ok(db) => {
      db.put(b"my key", b"my value");

      db.get(b"my key").map( |value| {
        match value.to_utf8() {
          Some(v) =>
            println!("retrieved utf8 value {}", v),
          None =>
            println!("did not read valid utf-8 out of the db"),
        }
      }).on_absent(|| { println!("value not found") });

      db.delete(b"my key");

      db.close();
    },
    Err(e) => panic!(e),
  }
}
```

### status
  - [x] basic open/put/get/delete/close
  - [x] linux support
  - [x] rocksdb compiled via cargo
  - [x] OSX support
  - [ ] column family operations
  - [ ] LRU cache
  - [ ] destroy/repair
  - [ ] batch
  - [ ] iterator
  - [ ] create/release snapshot
  - [ ] range
  - [ ] rustic merge operator
  - [ ] compaction filter, style
  - [ ] comparator
  - [ ] slicetransform
  - [ ] logger
  - [ ] windows support

Feedback and pull requests welcome!
