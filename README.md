# Token Standards Working Group

## Mission Statement

This working group is concerned with all aspects related to token and ledger standards. The group is the merger of the former "Ledger and Token" and "NFT" Working Groups. This repository is used to collaborate, document decisions, discuss changes, raise issues, and provide feedback.

## Process

The following process is followed for standards within this working group.

If you have a good idea or a need for a standard, feel free to join a meeting or bring it up on the [forum][FORUM]
or [Discord][DISCORD].

Keep in mind it should be related to token standards on the IC to be picked up. If you have other
ideas, still feel free to reach out, and we'll try to help you find the right working group.

These ideas are then translated into the draft standards by their original contributor and/or with help of members
within this working group. Draft standards enable developers to create early reference implementations.

Approved standards are actively being implemented by developers and are candidates for an official ICRC standard once
adoption has reached an adequate level.

| Status        | Description                                       |
|---------------|---------------------------------------------------|
| ![IDEA]       | Ongoing idea in meetings, on the forum, or Discord |
| ![ISSUE]      | Topic is under discussion in either an issue or PR   |
| ![DRAFT]      | Draft of the final standard, subject to change    |
| ![APPROVED]   | Approved standard within the working group        |
| ![STANDARD]   | Official NNS approved ICRC Standard               |
| ![ON HOLD]    | Waiting to be picked up again once prioritized    |
| ![UNKNOWN]    | Hasn't progressed and/or had updates for a while  |
| ![ABANDONED]  | Abandoned and is no longer actively pursued       |
| ![SUPERSEDED] | Another standard has replaced this standard       |

## Token Standards


### Ledger Standards
| Standard | Title                             | Status     | Lead       |
|----------|-----------------------------------|------------|------------|
| [ICRC-1](https://github.com/dfinity/ICRC-1/tree/main/standards/ICRC-1) | Token Standard  | ![STANDARD] | Roman |
| [ICRC-2](https://github.com/dfinity/ICRC-1/tree/main/standards/ICRC-2)  | Approve and Transfer From  | ![STANDARD] | Roman |
| [ICRC-3](https://github.com/dfinity/ICRC-1/blob/main/standards/ICRC-3/README.md) | Block Log  | ![STANDARD] | Mario |
| [ICRC-103](https://github.com/dfinity/ICRC-1/pull/197)  | List Outstanding Approvals            | ![APPROVED] | Bogdan |
| [ICRC-106](https://github.com/dfinity/ICRC-1/pull/196)   | Legacy Index Discovery | ![APPROVED] | Bogdan |
| [ICRC-107](https://github.com/dfinity/ICRC/pull/117) | Fee Collection  | ![APPROVED] | Bogdan |
| [ICRC-122](https://github.com/dfinity/ICRC/pull/125) | Blocks for Authorised Mints and Burns  | ![Draft] | Bogdan |
| [ICRC-123](https://github.com/dfinity/ICRC/pull/134) | Blocks for Authorised Freezing and Unfreezing  | ![Draft] | Bogdan |
| [ICRC-124](https://github.com/dfinity/ICRC/pull/135) | Blocks Stopping, Unstopping, Deactivating a Ledger | ![Draft] | Bogdan |


| Standard | Title                             | Status     | Lead       |
|----------|-----------------------------------|------------|------------|
| [ICRC-7](https://github.com/dfinity/ICRC/blob/main/ICRCs/ICRC-7/ICRC-7.md)  | Minimal Non-Fungible Token (NFT) Standard            | ![STANDARD] | [Lead Name] |
| [ICRC-37](https://github.com/dfinity/ICRC/blob/main/ICRCs/ICRC-37/ICRC-37.md)  | Approval Functionality for the ICRC-7 Non-Fungible Token (NFT)             | ![STANDARD] | [Lead Name] |
| [ICRC-97](https://github.com/dfinity/ICRC/pull/98)  | NFT Metadata              | ![APPROVED] | [Lead Name] |

### Naming and Namespacing Standards

| Standard | Title                                       | Status     | Lead       |
|----------|-------------------------------------------|------------|------------|
| [ICRC-113](https://github.com/dfinity/wg-token-standards/pull/1) | ICP Network Registry | ![Draft] | [Lead Name] |
| ICRC-XX  | Namespacing for `icp` URI scheme | ![Idea] | [Lead Name] |

### CAIP Compatibility Standards

| Standard | Title                                       | Status     | Lead       |
|----------|-------------------------------------------|------------|------------|
| [CAIP-2-compliant blockchain identifiers](https://github.com/dfinity/wg-token-standards/pull/2) | CAIP-2-compliant blockchain identifiers | ![Draft] | [Lead Name] |
| [CAIP-10-compliant account addresses](https://github.com/icvc/icp-namespace/pull/1) | CAIP-10-compliant account addresses | ![Draft] | [Lead Name] |

### Payment and Other Token-related Standards

| Standard | Title                                       | Status     | Lead       |
|----------|-------------------------------------------|------------|------------|
| [ICRC-22](https://github.com/dfinity/ICRC/pull/101/files) | URI Format for Payment Requests | ![Draft] | [Lead Name] |
| [ICRC-91](https://github.com/dfinity/ICRC/pull/96/files) | URI Scheme for Addressing Canister Content via HTTP | ![Draft] | [Lead Name] |

## Meetings and Community Participation

### Meeting Schedule
Meetings occur bi-weekly, Tuesdays 5pm CET (See [Calendar](https://calendar.google.com/calendar/u/0/embed?src=c_cgoeq917rpeap7vse3is1hl310@group.calendar.google.com&ctz=Europe/Zurich)).

- **Calendar:** Subscribe [here](https://calendar.google.com/calendar/u/0?cid=Y19jazBncjc5YmtnY29vaWNuMXA4N21vMWVyb0Bncm91cC5jYWxlbmRhci5nb29nbGUuY29t)
- **Agenda:** Posted before each meeting on the [Forum]
- **Recordings:** Available [here](https://drive.google.com/drive/u/0/folders/1TlaDISjZpAKpqJdXzYMw4hhuKj5YxZ3J)


### Discussion Channels
Join discussions on the `#token-standards` channel on [Discord].

## Contributing

We welcome contributions from the community!

### How to Contribute
- **Join Meetings:** Participate in bi-weekly calls.
- **Propose a Standard:** Open an issue with a detailed proposal.
- **Give Feedback:** Engage in discussions on the forum and review drafts.
- **Submit a PR:** Improve documentation and draft standards.

[//]: # (Status badges)

[IDEA]: https://img.shields.io/badge/STATUS-IDEA-29abe2.svg

[ISSUE]: https://img.shields.io/badge/STATUS-ISSUE-e7a237.svg

[DRAFT]: https://img.shields.io/badge/STATUS-DRAFT-f25a24.svg

[APPROVED]: https://img.shields.io/badge/STATUS-APPROVED-ed1e7a.svg

[STANDARD]: https://img.shields.io/badge/STATUS-STANDARD-572785.svg

[ON HOLD]: https://img.shields.io/badge/STATUS-ON_HOLD-222222.svg

[UNKNOWN]: https://img.shields.io/badge/STATUS-UNKNOWN-222222.svg

[ABANDONED]: https://img.shields.io/badge/STATUS-ABANDONED-222222.svg

[SUPERSEDED]: https://img.shields.io/badge/STATUS-SUPERSEDED-222222.svg

[//]: # (Common links)

[FORUM]: https://forum.dfinity.org/t/39900

[DISCORD]: https://discord.internetcomputer.org/

[CALENDAR]: https://calendar.google.com/calendar/u/0/embed?src=c_cgoeq917rpeap7vse3is1hl310@group.calendar.google.com

[RECORDINGS]: https://drive.google.com/drive/u/0/folders/1TlaDISjZpAKpqJdXzYMw4hhuKj5YxZ3J
