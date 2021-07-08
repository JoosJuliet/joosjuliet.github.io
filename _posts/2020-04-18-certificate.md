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

간편하게 인증서 취득
AWS Certificate Manager는 웹 사이트 또는 애플리케이션에 대한 SSL/TLS 인증서를 취득하는 데 필요한 시간 소모적이고 오류가 발생하기 쉬운 단계를 없애줍니다. 키 페어 또는 CSR(Certificate Signing Request)을 생성하거나, CSR을 인증 기관에 제출하거나, 취득한 인증서를 업로드 및 설치할 필요가 없습니다. AWS Management Console에서 클릭 몇 번으로 AWS에서 신뢰할 수 있는 SSL/TLS 인증서를 요청할 수 있습니다. 인증서가 생성되면, AWS Certificate Manager에서 인증서 배포를 처리하므로 사용자가 웹 사이트 또는 애플리케이션에 대해 SSL/TLS를 활성화할 수 있습니다.


AWS Certificate Manager는 AWS 서비스 및 연결된 내부 리소스에 사용할 공인 및 사설 SSL/TLS(Secure Sockets Layer/전송 계층 보안) 인증서를 손쉽게 프로비저닝, 관리 및 배포할 수 있도록 지원하는 서비스입니다. SSL/TLS 인증서는 네트워크 통신을 보호하고 인터넷상에서 웹 사이트의 자격 증명과 프라이빗 네트워크상에서 리소스의 자격 증명을 설정하는 데 사용됩니다. AWS Certificate Manager는 SSL/TLS 인증서를 구매, 업로드 및 갱신하는 데 드는 시간 소모적인 수동 프로세스를 대신 처리합니다.

AWS Certificate Manager에서는 사용자가 신속하게 인증서를 요청하고, Elastic Load Balancer, Amazon CloudFront 배포, API Gateway 기반 API와 같은 ACM 통합 AWS 리소스에 배포한 후, AWS Certificate Manager가 인증서 갱신을 처리하도록 할 수 있습니다. 또한, 내부 리소스에 대한 사설 인증서를 생성하고 중앙에서 인증서 수명 주기를 관리할 수도 있습니다. ACM 통합 서비스에 사용하도록 AWS Certificate Manager를 통해 프로비저닝한 공인 및 사설 인증서는 무료입니다. 애플리케이션을 실행하기 위해 생성한 AWS 리소스에 대한 비용만 지불하면 됩니다. AWS Certificate Manager Private Certificate Authority를 사용하면 사설 CA 작업과 발급한 사설 인증서에 대해 매월 요금을 지불하게 됩니다.

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
https://aws.amazon.com/ko/certificate-manager/
