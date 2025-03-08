# rust_compile_optimizations_cheatsheet

Note: you can put both/all build options in the cargo.toml, then use either build line.

## To build: Performance
```bash
cargo build --profile release-performance
```

# example optimizing for runtime speed using the binary:
#### To be put in the cargo.toml file...
```toml
[profile.release-small]
inherits = "release"
# Enable Link Time Optimization for size reduction
lto = true
# Single codegen unit for better optimization
codegen-units = 1
# Strip all symbols to reduce size
strip = "symbols"
# Use abort to eliminate unwinding code
panic = "abort"
# Disable incremental compilation
incremental = false
# Optimize for size over speed
opt-level = "z"
# Disable debug info completely
debug = false
# Disable rpath to save some bytes
rpath = false

# Apply the same size optimizations to all dependencies
[profile.release-small.package."*"]
opt-level = "z"
codegen-units = 1
strip = "symbols"
debug = false
```


## To build: Small-size Binary
```bash
cargo build --profile release-small 
```

# Optimized Small Binary Profile for Rust
#### To be put in the cargo.toml file...
```toml
[profile.release-small]
inherits = "release"
# Enable Link Time Optimization for size reduction
lto = true
# Single codegen unit for better optimization
codegen-units = 1
# Strip all symbols to reduce size
strip = "symbols"
# Use abort to eliminate unwinding code
panic = "abort"
# Disable incremental compilation
incremental = false
# Optimize for size over speed
opt-level = "z"
# Disable debug info completely
debug = false
# Disable rpath to save some bytes
rpath = false
# Apply the same size optimizations to all dependencies
[profile.release-small.package."*"]
opt-level = "z"
codegen-units = 1
strip = "symbols"
debug = false
```
