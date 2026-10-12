# PKI Build using Smallstep CA and OpenSSL
Building a Complete Public Key Infrastructure (PKI) Using Smallstep + OpenSSL
This project demonstrates the full lifecycle of creating a functional PKI on Windows using Smallstep CA and OpenSSL. The setup includes a root CA, an intermediate CA, a user certificate, and full chain verification.

1. Initialize the Certificate Authority
Using Smallstep:
Created a root CA (self‑signed trust anchor)
Created an intermediate CA (signed by the root)
Protected private keys with passphrases

Generated CA configuration:
2. Generate CSR + Private Key
Created a CSR and private key for:
CN = gerald.mokwe.ucll.be

Code:
step certificate create gerald.mokwe.ucll.be gerald.mokwe.csr gerald.mokwe.key --csr

3. Sign the Certificate
With the CA running:

Code:
step-ca "$(step path)\config\ca.json"
Signed the CSR:

Code:
step ca sign gerald.mokwe.csr gerald.mokwe.crt

4. Verify the Certificate Chain
Copied CA certificates:

Code:
root.pem
intermediate.pem

Verified with OpenSSL:

Code:
openssl verify -CAfile root.pem -untrusted intermediate.pem gerald.mokwe.crt
Result:

Code:
gerald.mokwe.crt: OK
