# pam-auth [![Version](https://img.shields.io/crates/v/pam-auth.svg)](https://crates.io/crates/pam-sys) [![Build Status](https://travis-ci.org/MrFloya/pam-auth.svg)](https://travis-ci.org/MrFloya/pam-auth)

Safe Rust bindings to Linux Pluggable Authentication Modules (PAM).
Currently only supports basic username/password authentication.

[Documentation @ gh-pages](https://mrfloya.github.io/pam-auth/)

## Note about stability
This crate follows [semantic versioning](http://semver.org). As such all versions below `1.0.0` should be
considered development versions. This means the API could change any time.

## Usage
1. Add `pam-auth` to your Cargo.toml:
```toml
[dependencies]
pam-auth = "0.2.0"
```
2. Use the `Authenticator` struct to authenticate and open a session
```rust
extern crate pam_auth;
pub fn main() {
        let service: "<yourapp>";
        let user: "<user>";
        let password: "<pass>";

        let mut auth = pam_auth::Authenticator::new(service);
        auth.set_credentials(user, password);
        if auth.authenticate().is_ok() && auth.open_session().is_ok() {
            println!("Successfully opened a session!");
        }
        else {
            println!("Authentication failed =/");
        }
}
```

## TODO:
  - [x] Implement basic user/password authentication
  - [x] Add `Authenticator` struct
  - [ ] Add documentation
  - [ ] Verify current `conv` does not leak memory
  - [ ] Allow custom `conv` functions to be passed (in pam-sys?)
  - [ ] Code cleanup

## License

Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual licensed as above, without any additional terms or
conditions.
