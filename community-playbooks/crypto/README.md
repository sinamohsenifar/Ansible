# Manage SSL Certificates with Ansible

This Ansible playbook automates the management of SSL certificates, including generating a Certificate Authority (CA), creating self-signed certificates, and signing a Certificate Signing Request (CSR) with the CA.

## Prerequisites

- Ensure that the `community.crypto` collection is installed:

```
    ansible-galaxy collection install community.crypto
```



## Playbook Overview

The playbook performs the following tasks:

1. Ensures the output directory exists.
2. Generates a private key for the CA.
3. Generates a CA certificate.
4. Generates a private key for the server certificate.
5. Generates a self-signed certificate.
6. Creates a Certificate Signing Request (CSR).
7. Signs the CSR with the CA.
8. Bundles the server private key and signed certificate into a PEM file.
9. Creates a PKCS#12 (PFX) file containing the private key and signed certificate.
10. Extracts certificates and key from the PKCS#12 file.

### Directory Structure

The output of the playbook is stored in the specified `output_directory`. The directory structure will look like this:

/your_path/Ansible/community-playbooks/crypto/output/ 
```
└── gitlab
    ├── ca.crt
    ├── ca.key
    ├── gitlab.crt
    ├── gitlab.key
    ├── gitlab.csr
    ├── signed.crt
    ├── gitlab.pem
    ├── keystore.p12
    └── keystore.pem
```

### Directory Structure

The output of the playbook is stored in the specified `output_directory`. The directory structure will look like this:

/your_path/Ansible/community-playbooks/crypto/output/ └── gitlab ├── ca.crt ├── ca.key ├── gitlab.crt ├── gitlab.key ├── gitlab-csr-private.key └── gitlab.csr



## Usage
- Running the Playbook
    To run the playbook, execute the following command:


```
    ansible-playbook community-playbooks/crypto/generate-self-signed-cert.yml
```


## Variables

The following variables are defined in the playbook:

- `output_directory`: The directory where the certificates and keys will be stored.
- `name`: The base name for the certificate files.
- `ca_name`: The common name for the CA certificate.
- `common_name`: The common name for the server certificate.
- `serial_number`: The serial number used in the certificate.
- `pfx_passphrase`: The passphrase for the PKCS#12 (PFX) file.
