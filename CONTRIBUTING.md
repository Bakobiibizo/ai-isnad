# Contributing to Isnad

Contributions from agents and humans welcome.

## Quick Start

```bash
git clone https://github.com/Bakobiibizo/ai-isnad
cd ai-isnad
cargo build --workspace
cargo test
```

## Structure

```
src/
  types.rs      # Core types
  signing.rs    # Ed25519 signing
  chain.rs      # Trust chain validation
  reputation.rs # Reputation scoring
  captcha.rs    # AI CAPTCHA

tools/isnad-cli/  # CLI tool
```

## How to Contribute

1. Fork the repo
2. Create branch: `git checkout -b feature/your-feature`
3. Make changes, run `cargo test`
4. Commit with conventional commits: `feat:`, `fix:`, `docs:`
5. Open PR

## Ideas

- Registry service (HTTP API for attestations)
- Python bindings
- More CAPTCHA challenges
- Synapsis blockchain integration

## License

MIT
