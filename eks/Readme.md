To create eks cluster in automode
# ekctl create cluster --name= <<cluster name>> --enable-auto-mode
We can also provide
-> --node=3
-> --nodes-min=2, --nodes-max=5
-> --region us-west-2
-> --node-type t3.medium
-> --managed/fargate

To delete cluster
eks delete cluster --name my-cluster

DNS BINDING
To domain bind
```bash
apt update
apt install bind9 dnsutils
apt update
apt install dnsutils
```

Enable in firewall
```bash
firewall-cmd--add-service=dns --permanent
firewall-cmd --reload
```

Edit config file
/etc/bind/named.conf.options
Add your global options here:
```bash
options {
    directory "/var/cache/bind";

    listen-on port 53 { any; };
    listen-on-v6 { any; };

    allow-query { any; };

    recursion yes;

    dnssec-validation auto;
};
```
 /etc/bind/named.conf.local
 Add your custom zone here:
 ```bash
zone "mywebapp.com" IN {
    type master;
    file "/etc/bind/mywebapp.com.fzone";
    allow-query { any; };
};
```
Create /etc/bind/mywebapp.com.fzone
```bash
$TTL 86400

@   IN  SOA ns1.mywebapp.com. admin.mywebapp.com. (
        2026062801
        3600
        1800
        604800
        86400
)

@       IN  NS      ns1.mywebapp.com.

ns1     IN  A       192.168.1.10
@       IN  A       192.168.1.10
www     IN  A       192.168.1.10
```

# To check confirm changes
```bash
named-checkconf
```
Start Bind
```bash
named -g
```

# Add in /etc/resolve.conf
To target our dns server
```
search localdomain
nameserver < your ip value >
```
