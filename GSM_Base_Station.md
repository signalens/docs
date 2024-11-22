# 0x00 DragonOS
Download DragonOS from https://cemaxecuter.com and install to hard disk
![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124201200.jpeg)

# 0x01 OpenBTS
The official version is too old, so here we choose to update it to support Ubuntu 20.04 and 22.04 versions

official version: https://github.com/RangeNetworks/openbts

changed version: https://github.com/PentHertz/OpenBTS

```bash
git clone https://github.com/PentHertz/OpenBTS
cd OpenBTS
sudo ./preinstall.sh

./autogen.sh
./configure --with-uhd
make -j$(nproc)
sudo make install
sudo ldconfig

uhd_usrp_probe 

sudo smqueue &
sudo sipauthserve &
sudo /OpenBTS/OpenBTS
```

Open another terminal
```
/OpenBTS/OpenBTSCLI
```

Setting up unauthenticated registration
```
config Control.LUR.OpenRegistration .*
```

Set the mobile network to 2G mode and search for the network

![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124220043.jpeg)
![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124215951.jpeg)

Close Service
```
fuser -k /usr/local/sbin/sipauthserve
fuser -k /usr/local/sbin/smqueue
```
# 0x02 osmo-nitb
DragonOS has osmo-nitb installed by default
```bash
cd /usr/src/osmo-nitb-scripts
vi config.json
```
Change enabled of call to true so that you can make calls

![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124231658.jpeg)

```
./main_uhd.py -h uhd --sip
```

Open another terminal
```
uhd_usrp_probe
/usr/bin/osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg
```

Mobile phone can access the network

![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124230417.jpeg)

After the mobile phone is connected to the network, the record can be seen on the terminal, as well as the assigned mobile phone number
![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124230200.jpeg)

Based on the assigned phone number, you can make a call

![SignalSDR Pro](https://github.com/signalens/signalsdrpro_docs/blob/main/img/Pasted%20image%2020241124230428.jpeg)
