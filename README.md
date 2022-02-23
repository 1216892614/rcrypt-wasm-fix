# `rcrypt`: A compact hashing and salting library based on bcrypt with smaller hashes

`rcrypt`, short for "reduced crypt" is a compact hashing and salting library based on bcrypt **generating hashes that are 33.3% smaller than bcrypt**. It was originally made for
a part of [Skytable](https://github.com/skytable/skytable)'s authentication system storage, but
was moved into a separate library for usage in the wider Rust community.
`rcrypt` is almost a drop-in replacement for the `bcrypt` crate.

The smaller hash sizes are achieved by rcrypt's
implementation of a hash+salt compression/decompression algorithm based on the [BMCF spec](https://github.com/ademarre/binary-mcf). The hashes produced are binary hashes.

## Usage

```rust
use rcrypt::DEFAULT_COST;
// your password
let mypass = String::from("pass123");
// hash
let hash = rcrypt::hash(&mypass, DEFAULT_COST).unwrap();
// verify
assert!(rcrypt::verify(&mypass, &hash).unwrap());
```

The usage remains just the same for users who use the [bcrypt](https://crates.io/crates/bcrypt) crate, except that the `hash` method returns a `Vec<u8>` instead of a `String`, while for the `verify` method you need to pass a `&[u8]` for the hash.

## License

This crate is distributed under the [Apache-2.0 License](./LICENSE).