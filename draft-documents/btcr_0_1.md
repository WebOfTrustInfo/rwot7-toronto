# BTCR v0.1 Decisions

Authors: Dan Pape, Ryan Grant, Christopher Allen, Kim Duffy, Anthony Ronning, Ganesh Annan, Wolf McNally

## Goal

Lock down BTCR v0.1. Decisions follow.

## Out of scope

### 1. Assume P2PKH

Other script types out of scope:
- P2SH
- Segwit

Why? Finding public key is harder

### 2. Only a URL in OP_RETURN

- NO IPFS
- IPFS lib in iPhone is a non-starter
	- has to be running at the time
	- requires persistence
- Mutable storage only

### 3. Extended DDO in github

### 4. Testnet only

## Credentials 

### 1. Use JSON-LD 1.1 javascript lib, because 0.1 doesn't need hardcore verifiers
### 2. Restrict to schema.org schemas. Can use Christopher's test cases
### 3. Privacy: stick to pseudoanonymous claim content
### 4. Restrict to VCs I wish to share

## Wallet functionality

### 1. ID Keys distinct from DIDs in wallet

### 2. Transactions

Base tx doesn't need to broadcast/fund TX to set initial funds (tx_0). Only needs to create TXs for tx_n (n>0) 

### 3. Tip following

- Ideally follow best practice BIP 157/158. Problem is that libraries not necessarily available. 
- Fallback is Kulpreet's REST service.

About BIP 157/158
- Neutrino
- Lightning branch of Go code
- Not as efficient as SPV: SPV requests lists of addresses it cares about. Neutro slower because it attempts to hide addresses it cares about.

## BTCR behavior decisions

### 1. Verification keys

- TXIn key only verifies DDOs
- TXOut key: 
	- if OP_RETURN exists and points to continuation DDO
		- TXOut key has no implication
		- Just accept continuation DDO
	- if dn exist
		- TXOut key can be used to verify verifiable credentials

### 2. No OP_RETURN after a TX means revoked
