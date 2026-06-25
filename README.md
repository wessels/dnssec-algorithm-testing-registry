# DNSSEC Algorithm Testing Registry

There is now a lot of interest to test post-quantum cryptography signing
algorithms in DNSSEC.  Such testing will require a way to identify
and distinguish candidate PQ algorithms.  One approach would be to
write Internet Drafts and get (permanent) assignments in IANA's DNSSEC
Algorithm Numbers registry.  The downside of that approach is that very
few of the candidate algorithms have been standardized at this point,
and when they do become standardized, they may change.

For example, FALCON is expected to be standardized by NIST but some of
the details might change before standardization is complete. This could
cause there to be multiple assignments for the same algorithm (old and
final), and thus possible operational issues and confusion about which
algorithm number means what.

We propose that testing not-yet-chosen algorithms can be done using
"PRIVATEDNS" algorithm 253, combined with the unofficial registry
maintained as a table in this document.

In the PRIVATEDNS scheme, signature and keys are prefixed with a domain
name to indicate the private algorithm being used. This name-to-algorithm
registry enables collaboration between multiple parties and can be used
by developers both to test and to get partners to test with them.


For testing purposes, there is an advantage if the keys and signatures
associated with an algorithm have sizes as close as possible to the final algorithms.
To maximize flexibility, the PRIVATEDNS names should be as short as possible.
Instead of following the recommendation in RFC 4034, for this unofficial
testing we propose that each algorithm be identified with a single-letter
domain name. For example, an algorithm that is identified as "{." would
use algorithm number 253 and the first three bytes of the key or signature
field would begin with 0x017b00. This makes all processing of algorithm
253 in this testing only need to check that the first byte is 0x01, the
third byte is 0x00, and that the second byte is recognized. Other uses of
algorithm 253 could proceed as they are now because, if they are following
the suggestion from RFC 4034, the names will all be longer than one
character.

The fields of this informal registry are:

* Name:        Domain name used to identify the algorithm plus the hex equivalent
* Description: Short description of algorithm
* URL:         URL to description of the algorithm
* Notes:       Notes on testing
* Author:      Name and email of the submitter

| Domain name and hex equivalent | Description | URL | Notes | Author |
| ------------------------------ | ----------- | --- | ----- | ------ |
| "2." (0x013200) | Keys and signatures are 2048 bytes | <https://www.proper.com/dnssec-2048.txt> | Used to always go to TCP with no validation overhead | [Paul Hoffman](mailto:phoffman@proper.com) |