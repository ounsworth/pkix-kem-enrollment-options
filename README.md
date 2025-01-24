# PKIX KEM Enrollment Mechanisms

## Do we need a Design Team?

I feel like 90% of usecases will be solved with existing mechanisms:

* Server-generated keys, delivered in a p12
* CMPv3 direct / indirect
* That EE already has a signing cert, so use that to sign the KEM CSR.

In my opinion, what we need a design team to study is whether there really is anything important in that remaining 20% that requires us to invent a new KEM CSR mechanism.

## Options to be explored:

One-shot: 
(ie enrollment only requires one request-response exchange to the CA)

*	Server-generated private key; ex.: cert issuance returns a p12 with a private key in it.
*	Use an already-issued signing cert to sign the KEM CSR. \[7\]
*	Unsigned id-algNone \[24\]
 
Challenge-response Proof-of-Possession:
(ie requires at least two round-trips to the CA)

*	CMPv3 \[8\]
    * Direct PoP
    * Inderect PoP
*	CRMF CSR \[9\]
*	CMC-over-EST \[9a\]

# References

* \[7\]: draft-housley-lamps-private-key-attest-attr
* \[8\]: cmpv3 - draft-ietf-lamps-rfc4210bis
* \[9\] KEM PoP in CRMF – maybe does not exist yet?
* \[9a\]: draft-ietf-lamps-rfc5272bis
* \[24\]: draft-davidben-x509-alg-none

