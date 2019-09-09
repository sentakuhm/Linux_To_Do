# This is a netctl static ip settings on Arch Linux

### First stop any started services lik Networkmanager or dhcpcd:<br>
`sudo systemctl stop Networkmanager.service`<br>
`sudo systemctl stop dhcpcd@enp0s3.service`<br>

`sudo cp /etc/netctl/examples/ethernet-static /etc/netctl/enp0s3`<be>

`sudo vim /etc/netctl/enp0s3` then add:<br>
```
Description='A basic static ethernet connection'
Interface=enp0s3
Connection=ethernet
IP=static
Address=('192.168.1.110/24')
Gateway='192.168.1.1'
DNS=('1.1.1.1' '1.0.0.1')
```
### Now enable & start netctl:<br>
`sudo netctl enable enp0s3`<br>
`sudo netctl start enp0s3`

