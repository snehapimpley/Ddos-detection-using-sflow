# Ddos-detection-using-sflow

For implementation following steps were taken:

1.Download sFlow-RT:
wget https://inmon.com/products/sFlow-RT/sflow-rt.tar.gz
tar -xvzf sflow-rt.tar.gz

2.Install the Mininet Dashboard application:
sflow-rt/get-app.sh sflow-rt mininet-dashboard

3.Start.sh will run the shell script command to run the sFlow applicationmultipass exec mininet -- ./sflow-rt/start.sh -Dscript.file=../ryu.js

4. Run the Ryu application. 
multipass exec mininet -- ryu-manager --ofp-tcp-listen-port 6653 --wsapi-port 8081 --verbose --app-lists ryu.app.simple_switch_13 ryu.app.ofctl_rest

5. In another window Mininet topology will execute. The ping command is run to check the connectivity between the hosts of the topology created. A zero percentage drop depicts the complete connectivity between the hosts.
multipass exec mininet -- sudo mn --custom sflow-rt/extras/sflow.py --link tc,bw=10 --topo tree,depth=2 --controller=remote

6.mininet sneha$ multipass list
Name                    State             IPv4             Image
mininet                 Running           192.168.64.2     Ubuntu 18.04 LTS


7. For accessing the sFlow trend GUI, a local host is created using the command: http://vm-ip:8008/app/mininet-dashboard/html/index.html 

8.Perform attack using hping3
ininet> h1 hping3 --flood --udp -k -s 53 h3
HPING 10.0.0.3 (h1-eth0 10.0.0.3): udp mode set, 28 headers + 0 data bytes
hping in flood mode, no replies will be shown

