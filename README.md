# Jenkins in Ubuntu/Linux

## Installation of Jenkins in Ubuntu:

First we have to install jdk to the host.

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```

For instalation of Jenkins use below commands:

```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo dnf upgrade
# Add required dependencies for the jenkins package
sudo dnf install fontconfig java-17-openjdk
sudo dnf install jenkins
sudo systemctl daemon-reload
```

&#x20;For starting Jenkins use below commands:

```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

then browes the site using the link:&#x20;

{% embed url="http:server-ip:8080" %}

### Adding a slave machine:

For adding a slave host with the Jankins master host, first we need to install jdk to that slave host.

{% code fullWidth="false" %}
```markup
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```
{% endcode %}

Then create a directory where all necessary files will be present. In my case, I have created a directory in `/opt`

`mkdir /opt/jankins-slave`

Give the read-write permission to the directory

`chmode 755 /opt/jankins-slave`

In the Jenkins slave directory we need to create the public and private key. Go to the jenkins-slave directory

```
cd /opt/jamkins-slave
```

To generate the ssh key use below command:

```
ssh-keygen
```

In will generate the key and save into the below location:

```
/home/riad/.ssh/
```

It will ask for passphrase, In my case i havenot used any passphase, so I kept it blank. After that it will generate the private and public key.

For connect with the Jenkins master server we need to use the private key. So go to that directory and copy the private key

```
cd /home/riad/.ssh/
cat id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
b3rfryyuretg6zaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdz
NhAAAAAwEAAQAAAYEAq2gR8k5R8Lqmkas4cXbABSm8r5oL8D7DFZmxddVwKKiAm9jhSTiu
ZvSHBteUrriLZbkwxHp7up82mQa3JP++15gQ0SCL9BuJLshgN4ty3nFK7ZBXGjvgUbq9n2
xnt728KC+xtHQHk9N80ocXpIGR/9gHHSRa/UjJeagdTLoWLTe+1CLS+Mf89OXqZz6a6/H1
ow760QYYjpu9966Bt0hGTgcuHVXdKhLjL7xB/Z6KIru9SryaxwV4p9Z1pYhs+YTAI+GeU8
wF1oHJjAcP7dO0i9HAqbCyR94yufDSJErgQEo9c6vvGALVfhMJ8/9pMea+27QLQsiyUryH
yNI6eHXU77xqQs5cRRWtlqy+CAK95NozZdR2EqRaNnb2TUQNLHKt1jsG5oba62c8EGGj2A
t3sp5bS6dwLoJZmEGYVECZ8sBIFlFgpE793eF2R3YGAOP3iR+kkfh6O+1mmEoAo62MJa7c
YYI/K80opQbSPDfyN2l9U+os8rRtLUsCvQpdABYGattFgXHQAAAMEA1HCOcjtVbUgb31B/
MGsDph39ReJHjaDKbev+4WekUEtvnxSip92lTWeUDb3p8jDNShVv7ePBahRsPJS455mhKR
yl+govTzsEtIFA0ic/EABnpt3k4Pmv9KYA/cUNa5NVoLCKlmeYQlPLiUztSCACxeznhOB+
xc5/e3xsLqXANkgCnbeqTf2EuZmTIY6w5T9CGkUGZg1WExxDCe5Pb76rHXPqv/ILix95EZ
CgmiS1wX8mn27r/BAMPenR15vDwdjvAAAAwQDOjZcGrFIoIpNhRquM/hHfTZPcjlnJrnIh
jO2VBc+Q3cq56AhSlae7GSOFTX+nXUE4cbIuP3N2uPyNbPNcOCSEX4OTyRWnzpsDMS9IOS
ST9dNqm90QOBT5o0lWWjboPe4faxNf0HOq2JO6w29y13Dw1KndnXBChZuMGnkoKaE80OfW
PH/2uoND56mB8GwLmjDyp4yZV5bh2TBoWhEI9tN786kXFkZOC+KZvbOwQu9jWO4w9MhP3A
DWeweuBTBWKqcAAAAMcmlhZEBjaS1jZDAz79yuio4kdr4UGBw==
-----END OPENSSH PRIVATE KEY-----
```

No goto the Jenkins GUI,&#x20;

Dashboard > Manage Jenkins > Credentials > System > Global credentials (unrestricted)

then click `Add credentials`\
