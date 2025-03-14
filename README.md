# rust_compile_optimizations_cheatsheet

Note: you can put both/all build options in the cargo.toml, then use either build line.

## To build: Performance
```bash
cargo build --profile release-performance
```

# example optimizing for runtime speed using the binary:
#### To be put in the cargo.toml file...
```toml
# build with -> cargo build --profile release-performance
[profile.release-performance]
inherits = "release"
# Maximum Link Time Optimization for best performance
lto = "fat"
# Single codegen unit maximizes optimization opportunities
codegen-units = 1
# Keep debug symbols for profiling capabilities
strip = "none"
# Use unwinding for better error handling without sacrificing much performance
panic = "unwind"
# Disable incremental compilation for maximum optimization
incremental = false
# Maximum optimization for speed
opt-level = 3
# Include minimal debug info for better profiling without much size impact
debug = 1
# Enable more aggressive optimizations
overflow-checks = false

# Optimize dependencies with the same settings
[profile.release-performance.package."*"]
opt-level = 3
codegen-units = 1
debug = 1
# LTO cannot be specified in package profile
```


## To build: Small-size Binary
```bash
cargo build --profile release-small 
```

# Optimized Small Binary Profile for Rust
#### To be put in the cargo.toml file...
```toml
# build with -> cargo build --profile release-small
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


## Combined (put into cargo.toml and call either later)
```toml
# build with -> cargo build --profile release-performance
[profile.release-performance]
inherits = "release"
# Maximum Link Time Optimization for best performance
lto = "fat"
# Single codegen unit maximizes optimization opportunities
codegen-units = 1
# Keep debug symbols for profiling capabilities
strip = "none"
# Use unwinding for better error handling without sacrificing much performance
panic = "unwind"
# Disable incremental compilation for maximum optimization
incremental = false
# Maximum optimization for speed
opt-level = 3
# Include minimal debug info for better profiling without much size impact
debug = 1
# Enable more aggressive optimizations
overflow-checks = false

# Optimize dependencies with the same settings
[profile.release-performance.package."*"]
opt-level = 3
codegen-units = 1
debug = 1
# LTO cannot be specified in package profile

# build with -> cargo build --profile release-small
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
