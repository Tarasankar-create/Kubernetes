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


To domain bind
# sudo apt install bind bind-utils
  sudo systemctl start/stop/status named (named is the process or service name)
