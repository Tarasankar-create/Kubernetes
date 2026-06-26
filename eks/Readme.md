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
# sudo apt install bind bind-utils
# sudo systemctl start/stop/status named (named is the process or service name)

Enable in firewall
```bash
firewall-cmd--add-service=dns --permanent
firewall-cmd --reload
```

Edit config file
# vi /etc/named.conf
--> add your ip in listen on port 53 in connfig file
Add after the zone in config file
```bash
zone ""IN{
  type master;
  file "mywebapp.com.fzone";
  allow-query{any; };
};
```
# To check confirm changes
```bash
named-checkconf
```
# create mywebapp.com.fzone file in /var/named
# Write in this 
```bash
$TTL 2d    ; default TTL for zone
@         IN      SOA   ns1.example.com. hostmaster.example.com. (
                                2003080800 ; serial number
                                12h        ; refresh
                                15m        ; update retry
                                4d         ; expiry
                                2h         ; minimum
                                )
; name server RR for the domain
           IN      NS      ns1.example.com.
www        IN      A       192.168.254.7
