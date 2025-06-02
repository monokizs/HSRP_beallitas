# HSRP_beallitas
```
from netmiko import ConnectHandler

def set_hsrp(d, v):
    net_connect = ConnectHandler(**d)
    net_connect.enable()

    net_connect.send_config_set([
				"Interface GigabitEthernet0/0/1",
				"standby 1 ip 192.168.1.1",
				f"standby 1 priority {v['priority']}",
				"standby 1 preempt"
    ])

    net_connect.disconnect()

# Több eszköz adatai listában
devices = [
    {'host': '192.168.1.2', 'username': 'admin', 'password': 'admin', 'secret': 'cisco', 'device_type': 'cisco_ios'},
    {'host': '192.168.1.3', 'username': 'admin', 'password': 'admin', 'secret': 'cisco', 'device_type': 'cisco_ios'}
]

variables = [
    {'hostname':'R1','priority':'150'},
    {'hostname':'R3','priority':'100'}
]

# Csatlakozás minden eszközhöz
for device,var in zip(devices,variables):  
    set_hsrp(device,var)
```
