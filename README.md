# PKIX KEM Enrollment Mechanisms

## Do we need a Design Team?

I feel like 90% of usecases will be solved with existing mechanisms:

* Server-generated keys, delivered in a p12
* CMPv3 direct / indirect
* That EE already has a signing cert, so use that to sign the KEM CSR.

In my opinion, what we need a design team to study is whether there really is anything important in that remaining 20% that requires us to invent a new KEM CSR mechanism.


## KEM enrollment mechanisms available

One-shot: 
(ie enrollment only requires one request-response exchange to the CA)

1.	Server-generated private key; ex.: cert issuance returns a p12 with a private key in it.
2.	Use an already-issued signing cert to sign the KEM CSR. \[7\]
3.	Unsigned id-algNone \[24\]
 
Challenge-response Proof-of-Possession:
(ie requires at least two round-trips to the CA)

4.	CMPv3 \[8\]
    * Direct PoP
    * Inderect PoP
5.	CRMF CSR \[9\]
6.	CMC-over-EST \[9a\]


## KEM enrollment usecases to explore

* Encryption key is escrowed
  * Option 1 Server Generated Keys.
* EEs have first a signing cert and then later request an encryption cert over a non-interactive CSR interface.
  * Sign the encryption CSR with existing signing cert.
* EEs enroll simultaneously a pair of signing and encryption certs over a non-interactive CSR interface.
  * Submit a coupled pair of CSRs where the signing key signs both CSRs. Could use \[7\].
*  EEs require only an encryption cert with no signing cert
  * Is this commen? Can we even name a usecase like this?
  * This is solved if CMPv3 is the enrollment protocol.
  * Other CSR-based protocols (ACME, EST, custom) would either need a direct or indirect PoP mechanisms to be added to CRMF and/or PKCS#10, or be ok with "signing" the encryption CSR with id-algNone \[24\] and relying on a protocol-level authentication mechanism, and not caring about proving possession of the KEM key.
* Are there usecases where none of the above apply? For example one-shot, non-interactive CSR-based where EEs do not have any signing keys?
  * Can we find an actual in-the-wild example of this usecase?
  * Potentially this would require a standardized MAC-based CSR protection mechanism using some sort of enrollment secret, or some other way to protect and authenticate the KEM CSR.


# References

* \[7\]: draft-housley-lamps-private-key-attest-attr
* \[8\]: cmpv3 - draft-ietf-lamps-rfc4210bis
* \[9\] KEM PoP in CRMF – maybe does not exist yet?
* \[9a\]: draft-ietf-lamps-rfc5272bis
* \[24\]: draft-davidben-x509-alg-none

