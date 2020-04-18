---
layout: post
section-type: post
title: "개인 certificate 받는 법"
category: AWS
tags: [ 'AWS' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)

---

``` python
#Define the domain name

DOMAIN='cloudelligent.com'
SUBDOMAIN='vpn'

#Organization Details
COUNTRY='PK'
PROVINCE='Punjab'
LOCATION='Lahore'
DEPARTMENT='IT'
COMMONNAME='Self Signed Certificate'


# Define where to store the generated certs and metadata.
DIR="$(pwd)/tls"

# Optional: Ensure the target directory exists and is empty.
rm -rf "${DIR}"
mkdir -p "${DIR}"





# Create the openssl configuration file. This is used for both generating
# the certificate as well as for specifying the extensions. It aims in favor
# of automation, so the DN is encoding and not prompted.
cat > "${DIR}/openssl.cnf" << EOF
[req]
default_bits = 2048
encrypt_key  = no # Change to encrypt the private key using des3 or similar
default_md   = sha256
prompt       = no
utf8         = yes
# Speify the DN here so we aren't prompted (along with prompt = no above).
distinguished_name = req_distinguished_name
# Extensions for SAN IP and SAN DNS
req_extensions = v3_req
# Be sure to update the subject to match your organization.
[req_distinguished_name]
C  = "$COUNTRY"
ST = "$PROVINCE"
L  = "$LOCATION"
O  = "$DEPARTMENT"
CN = "$COMMONNAME"
# Allow client and server auth. You may want to only allow server auth.
# Link to SAN names.
[v3_req]
basicConstraints     = CA:FALSE
subjectKeyIdentifier = hash
keyUsage             = digitalSignature, keyEncipherment
extendedKeyUsage     = clientAuth, serverAuth
subjectAltName       = @alt_names
# Alternative names are specified as IP.# and DNS.# for IP addresses and
# DNS accordingly.
[alt_names]
IP.1  = 127.0.0.1
DNS.1 = "$SUBDOMAIN"."$DOMAIN"
DNS.2 = localhost
EOF

# Create the certificate authority (CA). This will be a self-signed CA, and this
# command generates both the private key and the certificate. You may want to
# adjust the number of bits (4096 is a bit more secure, but not supported in all
# places at the time of this publication).
#
# To put a password on the key, remove the -nodes option.
#
# Be sure to update the subject to match your organization.
openssl req \
  -new \
  -newkey rsa:2048 \
  -days 36500 \
  -nodes \
  -x509 \
  -subj "/C="$COUNTRY"/ST="$PROVINCE"/L="$LOCATION"/O="$DEPARTMENT"" \
  -keyout "${DIR}/CA.key" \
  -out "${DIR}/CA.crt"
#
# For each server/service you want to secure with your CA, repeat the
# following steps:
#

# Generate the private key for the service. Again, you may want to increase
# the bits to 4096.
openssl genrsa -out "${DIR}/"$DOMAIN".key" 2048

# Generate a CSR using the configuration and the key just generated. We will
# give this CSR to our CA to sign.
openssl req \
  -new -key "${DIR}/"$DOMAIN".key" \
  -out "${DIR}/"$DOMAIN".csr" \
  -config "${DIR}/openssl.cnf"

# Sign the CSR with our CA. This will generate a new certificate that is signed
# by our CA.
openssl x509 \
  -req \
  -days 3650 \
  -in "${DIR}/"$DOMAIN".csr" \
  -CA "${DIR}/CA.crt" \
  -CAkey "${DIR}/CA.key" \
  -CAcreateserial \
  -extensions v3_req \
  -extfile "${DIR}/openssl.cnf" \
  -out "${DIR}/"$DOMAIN".crt"

# (Optional) Verify the certificate.
openssl x509 -in "${DIR}/"$DOMAIN".crt" -noout -text

# Generate PFX For Windows
#openssl pkcs12 -export -out "$DOMAIN".pfx -inkey "$DOMAIN".key -in "$DOMAIN".crt

#https://aws.amazon.com/blogs/security/how-to-prepare-for-aws-move-to-its-own-certificate-authority/
```
---
참고: https://github.com/quickbooks2018/bash-scipts/blob/master/aws-self-signed-acm.sh
