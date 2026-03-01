# Influence Tactics Protocol (ITP)

An open standard for detecting, scoring, and communicating information manipulation in digital content.

## What is the ITP?

The Influence Tactics Protocol defines a **20-category assessment framework** organized into **5 composite factors**, producing a final **0–100 manipulation score**. It enables interoperable manipulation detection across platforms while preserving user autonomy and preventing censorship.

The protocol focuses on **teaching patterns, not declaring truth**. A high score indicates the presence of influence techniques, not necessarily misinformation.

## The 5 Composite Factors

| Factor | Categories | Weight |
|--------|-----------|--------|
| **Emotional Manipulation** | Emotional Triggers, Urgent Action Demands, Novelty Overuse, Emotional Repetition, Manufactured Outrage | 25% |
| **Suspicious Timing** | Timing Coincidence, Financial/Political Gain, Historical Parallels | 20% |
| **Uniform Messaging** | Phrase Repetition, Bandwagon Effect, Rapid Behavior Shifts | 20% |
| **Tribal Division** | Us vs. Them Dynamic, Simplistic Narratives, False Dilemmas | 15% |
| **Missing Information** | Context Omission, Authority Overload, Suppression of Dissent, Cherry-Picked Data, Logical Fallacies, Framing Techniques | 20% |

## Risk Tiers

| Score | Tier | Meaning |
|-------|------|---------|
| 0–25 | Low | Minimal influence tactics detected |
| 26–50 | Moderate | Some persuasion patterns present |
| 51–75 | High | Significant influence tactics detected |
| 76–100 | Severe | Heavy use of manipulation techniques |

## Design Principles

1. **Transparency** — All scoring methods must be explainable
2. **Interoperability** — Any system can implement the protocol
3. **Privacy** — No mandatory user tracking or identification
4. **Education** — Focus on teaching patterns, not declaring truth
5. **Decentralization** — No single point of control or failure

## Conformance Levels

| Level | Name | Requirements |
|-------|------|-------------|
| 1 | **ITP-Core** | All 20 categories scored (1–5), composite factors calculated, overall score (0–100) |
| 2 | **ITP-Validated** | Level 1 + multi-scorer consensus, validation API support |
| 3 | **ITP-Full** | Level 2 + all context providers, distributed validation network |

## Specification

The full protocol specification is available in [`itp-spec.md`](itp-spec.md).

## Reference Implementation

[Decipon](https://decipon.com) provides a reference implementation of the ITP at conformance Level 3 (ITP-Full).

## Acknowledgments

The scoring framework was inspired by publicly discussed work by Chase Hughes on influence and behavioral analysis. The ITP is an independent specification, not affiliated with or endorsed by Chase Hughes or any related organizations.

## License

This specification is released under the [MIT License](LICENSE).
