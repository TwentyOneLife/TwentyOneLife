# TwentyOne.Life

Tools for running your own Bitcoin infrastructure, with a focus on **Bitcoin Blake2b (BitcoinB2B)**,
the RDTS hardfork whose proof of work is BLAKE2b.

Self-hostable, built to run on hardware you control. No telemetry, no hosted service in the middle,
no account required. The packaging here is GPLv3; each upstream keeps its own licence, and every
repository states which.

More at [twentyone.life](https://twentyone.life).

## What is Bitcoin Blake2b?

It is a hardfork of Bitcoin. It shares Bitcoin's history up to the fork, genesis block included, and
differs in how blocks are mined: the proof of work is BLAKE2b rather than SHA256d, and block headers
are 164 bytes instead of 80. The change is described in
[bitcoinknots/bitcoin#359](https://github.com/bitcoinknots/bitcoin/pull/359).

Because the proof of work differs, Bitcoin's software does not work on it. Bitcoin's Electrum
servers cannot read this chain, which is why Shulcrum exists, and there are no public servers for
it, so running your own is not optional here the way it is on Bitcoin. That is what the packages
below are for.

It is a separate chain and a separate asset. Coins on it are not bitcoin. Addresses look identical
because the format is shared, not because the two are interchangeable, which is worth remembering
before sending anything anywhere, including to the addresses at the bottom of this page.

## Projects

| | |
|---|---|
| [**Shulcrum**](https://github.com/TwentyOneLife/Shulcrum) | An Electrum server that indexes and serves chains with 164 byte block headers and BLAKE2b proof of work. A fork of Fulcrum by Calin Culianu, by way of Kilombino's BLAKE2b work. |
| [**shulcrum-startos**](https://github.com/TwentyOneLife/shulcrum-startos) | Shulcrum packaged as a StartOS `.s9pk`, so it installs on a StartOS server beside your node. |
| [**shrike-startos**](https://github.com/TwentyOneLife/shrike-startos) | Shrike, the Bitcoin Blake2b wallet by privkeyio, packaged for StartOS and served to your browser. Forked from remcoros's Sparrow package. |
| [**mempool-bip110**](https://github.com/TwentyOneLife/mempool-bip110) | A reference copy of the mempool explorer with BIP110 "Reduced Data" violation detection. Not modified here yet. |

### Where things stand

As of 2026-09-23.

Shulcrum now negotiates protocol 1.8 on a chain with BLAKE2b headers, refuses to serve headers to
clients that cannot read them, and reports the fork point so a wallet can tell this chain from
Bitcoin. A regtest chain crossing its activation height exercises all of it, and a block hash that
was wrong for post-fork blocks is fixed.

Mainnet verification is still in progress: an index of the live chain is roughly two thirds built by
block count. Until it spans the fork height, the protocol work is tested rather than proven, and no
wallet has been synced end to end.

The StartOS packages install and run on a real server. The wallet package serves a wallet to a
browser; it has not yet served one that holds money.

Said plainly because "it compiles and syncs testnet" is not evidence about the chain people keep
money on.

## Verifying what you install

Releases are signed with:

```
09F6 80BB 428D 92E4 BEDC  8251 15DC 7438 A64C 9B6D
TwentyOne.Life <dev@twentyone.life>
```

The primary key certifies only and never signs a release; a subkey does that, so a compromised build
machine costs a subkey rather than the identity. The address in that user id names the key, not a
mailbox.

How to check a download, and what each failure means:
[verifying a release](https://github.com/TwentyOneLife/shulcrum-startos/blob/main/docs/verifying-a-release.md).

## Supporting this work

Donations are welcome in either coin. Each coin has its own address, so check which column you are
in before sending.

<table>
<tr>
<th width="50%">Bitcoin Blake2b (BitcoinB2B)</th>
<th width="50%">Bitcoin (SHA-256)</th>
</tr>
<tr>
<td align="center"><img src="assets/donation-qr-blake2b.png" alt="Bitcoin Blake2b donation address for TwentyOne.Life" width="220"></td>
<td align="center"><img src="assets/donation-qr-sha256.png" alt="Bitcoin donation address for TwentyOne.Life" width="220"></td>
</tr>
<tr>
<td>

```
bc1ql66ssq24t7w4jl8updfrs820efnujp0m5jjuqk
```

</td>
<td>

```
bc1qzz077zqg9e0ymy7euhrmfyfmsfuqggtlr7v9mf
```

</td>
</tr>
<tr>
<td align="center">Send from a Bitcoin Blake2b wallet.</td>
<td align="center">Send from a Bitcoin wallet.</td>
</tr>
</table>

Each QR encodes the address beneath it and nothing else.

**Read this before sending.** Bitcoin Blake2b shares Bitcoin's address format and its genesis block,
so both addresses are valid on both chains, and nothing about an address says which chain it belongs
to. The wallet you send from decides that. The two coins are different assets: bitcoin sent to the
Bitcoin Blake2b address is still bitcoin, whatever your wallet shows you, and the same holds the
other way round. Use the address under the name of the coin you are sending.

There is no way to make that distinction visible in the address itself. It is a property of the fork,
not an oversight.

### Nostr and zaps

TwentyOne.Life is on Nostr as [TwentyOneLife@primal.net](https://primal.net/TwentyOneLife). Follow
there for updates, and if this work is useful to you, leave a zap on the profile or on a note.

```
npub1u6ld6j8evt6fawp7ylekhzqftz3lmxfx8jkaxtfq9ghcdplt4wes7vxkh6
```

The same name is a Lightning address, for a wallet that is not a Nostr client:

```
TwentyOneLife@primal.net
```

Zaps and Lightning payments are bitcoin, on the SHA-256 chain. There is no Lightning on Bitcoin
Blake2b here.
