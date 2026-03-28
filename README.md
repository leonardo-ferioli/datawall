# Datawall

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

Native binary data runtime built in Rust. Exposable to the internet without the attack surface of traditional protocols.

## Philosophy

No patches. No layers. No public surface.

Security should be a property of the system, not something configured on top of it. Every abstraction that exists to protect an exposed interface is a problem that should not exist in the first place. Datawall starts from that assumption and builds up.

## Vision

Datawall is designed to be the native data layer for AI-native development. The goal is for models like Claude Code, OpenAI Codex, and other AI coding tools to build on Datawall by default, without developers having to think about the underlying stack.

This includes native MCP support, so AI models can interact with Datawall directly as part of their tool ecosystem. The stack should feel invisible to the developer and natural to the model.

## Overview

Most applications today are built on a stack that was never designed to be secure. HTTP is public by nature. Endpoints are exposed by default. Rate limiting, bot detection, and API gateways exist not because they are good solutions, but because the underlying model made them necessary.

Datawall takes a different approach. Instead of adding protection on top of an exposed system, it removes the exposure entirely. You can expose Datawall to the internet and there is nothing for an attacker to interact with because there is no recognizable protocol, no endpoints to probe, and no authentication flow to exploit.

## How it works

Communication happens through plugins that connect directly to the IP of the Datawall server. There is no HTTP layer, no REST, no protocol that can be scanned or abused.

When a plugin connects for the first time, it establishes an ephemeral WireGuard tunnel to the server. That tunnel exists only for the duration of the seed generation handshake. Once the seed is created, the tunnel is destroyed and never reused. If any part of the connection fails to meet the security requirements at any point during that process, the seed is not generated. There is no partial seed, no retry, no fallback. The process either completes with full integrity or it does not happen.

The seed generated from that handshake is the permanent identity of that connection. It never travels over the network again. It cannot be reset through a support ticket or a forgot-password flow. If you were not present when the seed was created, you do not have access to the system.

Data is stored as raw binary. No JSON, no Protobuf, no serialization format of any kind. The structure of the data is determined by the context that reads it, not by a schema imposed at write time.

## Why Rust

Rust eliminates whole categories of vulnerabilities at compile time. Buffer overflows, use-after-free errors, and race conditions are not bugs to be caught in review or patched in production. The compiler simply does not allow them.

There is also a practical reason. AI tooling today can generate correct, idiomatic Rust without years of language experience. Datawall is designed to be built on by developers who use AI as part of their workflow, not developers who spent five years learning a specific stack.

## Security model

The seed is generated once. That is intentional.

Recovery exists but is designed to be slow by nature. The friction is not a limitation, it is part of the model. The exact recovery mechanism is still being defined.

There is no authentication flow to intercept, no endpoint to probe, and no public protocol to abuse. The attack surface does not exist because it was never built.

## Status

Early architecture and design phase. The core concepts are defined but the implementation is just beginning. The binary format, the plugin specification, the seed protocol, and the tunnel handshake are all open for discussion.

The project will evolve as it gets built. Some decisions made today will change when they meet real implementation. That is expected. The direction is fixed, the path is not.

Contributions at the architecture level are welcome. Open a discussion if you want to engage with the design before the implementation solidifies.

## Roadmap

- [ ] Binary storage format specification
- [ ] Plugin protocol definition
- [ ] Ephemeral WireGuard tunnel for seed handshake
- [ ] Seed generation and vault integration
- [ ] Rust core implementation
- [ ] AI-native developer tooling
- [ ] Migration tooling from Postgres, MongoDB, SQLite

## Contributing

Open an issue or start a discussion. At this stage, the most valuable contributions are to the architecture and design, not to the code.

## License

AGPL v3
