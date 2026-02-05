# Isnad

Agent-to-agent attestation protocol with AI CAPTCHA.

*Named after Islamic hadith authentication - a claim is only as trustworthy as its chain of transmission (isnad).*

## Problem

skill.md files are unsigned code. Credential stealers have been found in skill repositories. The agent ecosystem lacks code signing, reputation systems, and provenance chains.

## Solution

- **Signed attestations**: Agents vouch for skills/agents with Ed25519 signatures
- **Trust chains**: Traverse who-vouched-for-whom back to trust anchors
- **Reputation scoring**: Aggregate attestations into meaningful scores
- **AI CAPTCHA**: Prove you're an agent, not a human

## Quick Start

```bash
cargo build --workspace

# Generate keypair
./target/debug/isnad keygen -o my.key -p my.pub

# Hash a skill
./target/debug/isnad hash skill.md

# Create attestation
./target/debug/isnad attest \
  --subject-hash "sha256:..." \
  --subject-name "weather-skill" \
  --agent-id "my-id" \
  --agent-name "MyAgent" \
  -t audit -k my.key

# Verify
./target/debug/isnad verify attestation.json -k my.pub
```

## AI CAPTCHA

Prove you're NOT human:

```bash
./target/debug/isnad captcha generate -o challenge.json --answers answers.json
# Complete challenge...
./target/debug/isnad captcha verify -c challenge.json -r response.json -a answers.json
```

## Library

```rust
use isnad::{Attestation, AttestationType, Attestor, Subject, KeyPair};

let keypair = KeyPair::generate();
let mut attestation = Attestation::new(
    Attestor {
        agent_id: keypair.public_key_id(),
        agent_name: "MyAgent".to_string(),
        platform: Some("moltbook".to_string()),
    },
    AttestationType::SecurityAudit,
    Subject::skill("weather-skill", "sha256:..."),
);
attestation.sign(&keypair)?;
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). PRs welcome.

## License

MIT
