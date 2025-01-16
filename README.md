# PKIX KEM Enrollment Mechanisms

Options to be explored:

One-shot: 
(ie enrollment only requires one request-response exchange to the CA)
•	Server-generated private key; ex.: cert issuance returns a p12 with a private key in it.
•	Use an already-issued signing cert to sign the KEM CSR. [7]
•	Unsigned id-algNone [24]
 
Challenge-response Proof-of-Possession:
(ie requires at least two round-trips to the CA)
•	CMPv3 [8]
  - Direct PoP
  - Inderect PoP
•	CRMF CSR [9]
•	CMC-over-EST [9a]

# References

[7]: draft-housley-lamps-private-key-attest-attr
[8]: cmpv3 - draft-ietf-lamps-rfc4210bis
[9] KEM PoP in CRMF – maybe does not exist yet?
[9a]: draft-ietf-lamps-rfc5272bis
[24]: draft-davidben-x509-alg-none

