# BCHostTrust (BCHT) - Blockchain-based website trustworthiness database

*by Marco Pui, Cato Yiu, Lewis Chen*

## Writer's Remark

This paper assumes knowledge of blockchain, especially Bitcoin. Consider reading the [Bitcoin paper](https://bitcoin.org/en/bitcoin-paper) before reading this.

## Abstract

In the digital era, websites play a crucial role in daily life, often associated with hostnames translated into IP addresses through DNS. However, the legitimacy of a website is not guaranteed, as scammers can create deceptive domains. BCHostTrust (BCHT) proposes a solution using a distributed database based on a Bitcoin-like blockchain to store the trustworthiness of hostnames. By leveraging the collective computation power of normal users, this system aims to increase the difficulty for scammers to manipulate search engine rankings. The blockchain employs SHA3-256 for hashing and implements a proof-of-work mechanism to deter malicious activities. The BCHT blockchain structure includes blocks containing hashed entries with voting attitudes (e.g., upvotes or downvotes) toward specific hostnames. This innovative approach seeks to enhance online security by crowdsourcing website trustworthiness evaluation through a decentralized and tamper-resistant blockchain system. <!-- By ChatGPT -->

## Introduction

In the information age, websites are serving important roles in daily life. They are usually associated with one or more hostnames and have them translated into the corresponding IP addresses via a Domain Name System (DNS). This ensures everyone can easily remember how to access a website without remembering a multi-digit chain of numbers.

Assume that the DNS is resolving the correct IP addresses, this does not imply that the website is legitimate. A scammer may register a domain name similar to its legitimate counterpart, for example, "whatapp&#46;com" pretending to be "whatsapp.com", and have it raised to the top of search engines via advertisements to fool careless persons.

In our solution, a distributed database based on Bitcoin-like Blockchain is used to store the trustworthiness of hostnames. Assuming the number of normal users is high enough, this can increase the difficulty for scammers to raise the rank of their scam website.

## The chain of hashed blocks

If you are familiar with Bitcoin, the concept of chaining data up should not be hard to understand. In the BCHostTrust blockchain, we also chain up blocks by cryptographic hashes, in out case, SHA3-256. This ensures blocks come one after another, forming a traceable chain.

```raw
  +-----------+        +-----------+        +-----------+        
  |  Block 1  |        |  Block 2  |        |  Block 2  |        
  +-----------+  hash  +-----------+  hash  +-----------+  hash  
--> prev_hash |--------> prev_hash |--------> prev_hash |-------> ...
  +-----------+        +-----------+        +-----------+        
  | ......... |        | ......... |        | ......... |            
  +-----------+        +-----------+        +-----------+        
```

## The data that comes with the block

In addition to the hash of the previous block, a BCHT block also contains a list of entries, each storing the following:

1. The hostname to be voted on; and
2. The attitude of the vote.

The attitude field stores what should this entry represent, for example, an upvote or a downvote.

## Proof-of-Work

To increase the cost of casting new blocks, a proof-of-work mechanism is introduced. Just like Bitcoin, the proof-of-work mechanism is implemented "by incrementing a nonce in the block until a value is found that gives the block's hash the required zero bit." As a result, if we assume the collective computation power of normal users is higher than that of scammers, a large board of normal users can build blocks relatively faster than scammers.

## Block exchange

After a new block is cast, it should be broadcast to other nodes. Upon receiving a new block, the node should work on it instead of the previous one. This is straightforward when it comes to linear block casting.

However, if a node receives multiple blocks with the same previous block, same as Bitcoin, "they work on the first one they received, but save the other branch in case it becomes longer." This ensures the wide-accepted chain would always be linear.

## Structure of BCHT Blockchain

### Structure of BCHT Block

* `version`: 2 bytes integer
* `prev_hash`: 32 bytes SHA3-256 hash of the previous block.
* `creation_time`: 8 bytes of 64-bit Unix epoch
* `nonce`: 4 bytes integer, increases on every proof-of-work attempt
* `entries`: Variable-length direct concatenate of BCHT Entries

### Structure of BCHT Entry

* `attitude`: 1 byte integer, the attitude of the entry
* `domain_name_len`: 4 byte integer, the length of the hostname. This is required because entries are directly concatenated after each.
* `domain_name`: Variable-length string of the hostname.
