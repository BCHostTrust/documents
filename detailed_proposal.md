# Blockchain-based website trustworthy database

## Summary
A blockchain can be used to determine whether a website is trustworthy. Proof-of-work mechanics can be implemented to keep scammers out of the system.

## Background:
Many people cannot distinguish between a legitimate website and a scam one. For example, a scam Whatsapp website can steal the account away and do whatever wanted by the attacker.
As TLS encryption is now popular, more and more websites are encrypted and have a padlock beside their URL. Unlike common belief, the "S" in HTTPS does not imply that the website is safe. ACME services such as Let's Encrypt issue SSL certificates for free for any servers that can verify their ownership of a hostname, so with a hostname that is very similar to the legitimate one, scammers can create fake websites while still keeping the padlock prepended before the URL.
So you might think, "Then we should completely remove the damn evil ACME!" However, there are two concerns. First, ACME allows amateur or low-budget websites to get their traffic encrypted, which, if removed, would be a huge drawback to cyber security. Second, some cloud service providers like Cloudflare are providing free SSL certificates from CAs apart from the ACME CAs. As a result, removing ACME would lead to worse circumstances.

## Existing solutions
The padlock besides the URL may be the most ancient attempt to solve this problem. By the time SSL certificates are still expensive to scammers, this kind of works. However, as mentioned above, TLS encryption is no longer the ideal identifier of trustworthy websites. More modern solutions maintain a database of scam websites, but they may not be collecting the data directly from end users. Also, they may not be able to verify the reliability of the data.

## My solution
A blockchain for website trustworthiness can be created. End-user's clients tell the system they have visited a certain website by appending a block onto the chain. By searching through the chain (one or some centralized servers can be set up for the low-performance end users), one can tell whether a website is trustworthy by seeing how many end users are visiting that website.
Now you may ask, "Can scammers spam records onto the chain, generating fake credibility for their scam website?" With the proof-of-work system built into the blockchain, the impact of those scam records can be ignorable. The proof-of-work will take a reasonable amount of time for normal visitors who create a reasonable amount of records in a period (real humans are limited to their speed and actual need to access websites), and a horrible amount of time for scammers to fake credibility from the ground up.

## Resources Needed
A server is needed to host websites, related executables, and the entire blockchain (at least for early-stage tests). 

