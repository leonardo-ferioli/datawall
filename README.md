# Datawall

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

Native binary data runtime built in Rust. No APIs, no tokens, no public surface to attack.

## Philosophy

No patches. No layers. No public surface.

Security should be a property of the system, not something configured on top of it. Every abstraction that exists to protect an exposed interface is a problem that should not exist in the first place. Datawall starts from that assumption and builds up.

## Overview

Most applications today are built on a stack that was never designed to be secure. HTTP is public by nature. Endpoints are exposed by default. Rate limiting, bot detection, and API gateways exist not because they are good solutions, but because the underlying model made them necessary.

Datawall takes a different approach. Instead of adding protection on top of an exposed system, it removes the exposure entirely.

## How it works

Communication happens through plugins, not endpoints. There is no HTTP layer, no REST, no protocol that can be scanned or abused.

Access is controlled by a cryptographic seed generated once at the moment of first connection. That seed never travels over the network. It cannot be reset through a support ticket or a forgot-password flow. If you were not present when the seed was created, you do not have access to the system.

Data is stored as raw binary. No JSON, no Protobuf, no serialization format of any kind. The structure of the data is determined by the context that reads it, not by a schema imposed at write time.

## Why Rust

Rust eliminates whole categories of vulnerabilities at compile time. Buffer overflows, use-after-free errors, and race conditions are not bugs to be caught in review or patched in production. The compiler simply does not allow them.

There is also a practical reason. AI tooling today can generate correct, idiomatic Rust without years of language experience. Datawall is designed to be built on by developers who use AI as part of their workflow, not developers who spent five years learning a specific stack.

## Security model

The seed is generated once. That is intentional.

Recovery is possible, but it is designed to be slow. It requires going through a documented human support process. The friction is not a limitation of the system, it is part of the security model. If recovering access takes weeks and leaves an auditable trail, most attacks stop being worth attempting.

There is no authentication flow to intercept, no endpoint to probe, and no public protocol to abuse. The attack surface does not exist because it was never built.

## Status

Early architecture and design phase. The core concepts are defined but the implementation is just beginning. The binary format, the plugin specification, and the seed protocol are all open for discussion.

The project will evolve as it gets built. Some decisions made today will change when they meet real implementation. That is expected. The direction is fixed, the path is not.

Contributions at the architecture level are welcome. Open a discussion if you want to engage with the design before the implementation solidifies.

## Roadmap

- [ ] Binary storage format specification
- [ ] Plugin protocol definition
- [ ] Seed generation and vault integration
- [ ] Rust core implementation
- [ ] AI-native developer tooling

## Contributing

Open an issue or start a discussion. At this stage, the most valuable contributions are to the architecture and design, not to the code.

## License

AGPL v3
