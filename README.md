# Documentacion
### Universidad de San Carlos de Guatemla  
### Facultad de Ingenieria
### Redes de Computadoras 1
### Practica 2

| Carnet | Nombre |
| ------ | ------ |
| 201503515 | César David Juárez González |
| 201503971 | Shubert Alexander Alonso Agustín |
| 201503723 | Bryan Gustavo Lopez Echeverria |
| 201503840 | Hugo René Figueroa Castillo |


# Topología 1
## Dispositivos

##### CLOUD
| CLOUD | Destino | Local Port | Remote Host | Remote Port |
| ------ | ------ | ------ | ------ | ------ |
| Cloud1 | Topología 2 | 30000 | 10.8.0.3 | 20000 |  


##### PUERTOS Y CONFIGURACIONES
| SWITCH | VTP MODE | PUERTOS | PORTCHANNEL | TIPO |
| ------ | ------ | ------ | ------ | ------ |
| ESW8 | CLIENT | f1/0,1 | Po1 | TRUNK |
| ESW8 | CLIENT | f1/4,5 | Po3 | TRUNK |
| ESW8 | CLIENT | f1/10 | -- | ACCESS |
| ESW9 | CLIENT | f1/0,1 | Po1 | TRUNK |
| ESW9 | CLIENT | f1/2,3 | Po2 | TRUNK |
| ESW9 | CLIENT | f1/10 | -- | ACCESS 
| ESW9 | CLIENT | f1/11 | -- | ACCESS 
| ESW9 | CLIENT | f1/12 | -- | ACCESS 
| ESW9 | CLIENT | f1/15 | -- | TRUNK 
| ESW10 | CLIENT | f1/2,3 | Po2 | TRUNK |
| ESW10 | CLIENT | f1/4,5 | Po3 | TRUNK |
| ESW10 | CLIENT | f1/10 | -- | ACCESS |

## Comandos utilizados
### EtherSwitch8  
```bash
conf t
int range f1/0 -1
channel-group 1 mode on
exit

conf t
int range f1/4 -5
channel-group 3 mode on
exit

int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005

int f1/10
switchport mode access
switchport access vlan 10

conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end
```
### EtherSwitch9  
```bash
conf t
int range f1/0 -1
channel-group 1 mode on
exit

conf t
int range f1/2 -3
channel-group 2 mode on
exit



int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005


int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005

int f1/15
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005


int f1/10
switchport mode access
switchport access vlan 20

int f1/11
switchport mode access
switchport access vlan 30

int f1/12
switchport mode access
switchport access vlan 30




conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end

```

### EtherSwitch10  
```bash
conf t
int range f1/2 -3
channel-group 2 mode on
exit


conf t
int range f1/4 -5
channel-group 3 mode on
exit


int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005


int f1/10
switchport mode access
switchport access vlan 10

conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end
```
### Topología 2

##### CLOUD
| CLOUD | Destino | Local Port | Remote Host | Remote Port |
| ------ | ------ | ------ | ------ | ------ |
| Cloud1 | Topología 3 | 40000 | 10.8.0.2 | 50000 |
| Cloud1 | Topología 1 | 20000 | 10.8.0.4 | 30000 |

##### PUERTOS Y CONFIGURACIONES
| SWITCH | VTP MODE | PUERTOS | PORTCHANNEL | TIPO |
| ------ | ------ | ------ | ------ | ------ |
| ESW1 | SERVER | f1/0,1,2 | Po2 | TRUNK |
| ESW1 | SERVER | f1/3,4,5 | Po3 | TRUNK |
| ESW1 | SERVER | f1/6,7 | Po1 | TRUNK |
| ESW1 | SERVER | f1/8 | N/A | TRUNK |
| ESW2 | CLIENT | f1/0,1,2 | Po5 | TRUNK |
| ESW2 | CLIENT | f1/3,4,5 | Po4 | TRUNK |
| ESW2 | CLIENT | f1/6,7 | Po1 | TRUNK |
| ESW3 | CLIENT | f1/0,1,2 | Po2 | TRUNK |
| ESW3 | CLIENT | f1/3,4,5 | Po4 | TRUNK |
| ESW3 | CLIENT | f1/6 | N/A | TRUNK |
| ESW4 | CLIENT | f1/0,1,2 | Po5 | TRUNK |
| ESW4 | CLIENT | f1/3,4,5 | Po3 | TRUNK |

##### VLANS
| VLAN | Nombre |
| ------ | ------ |
| 10 | ADMINISTRACION |
| 20 | CONTABILIDAD |
| 30 | VENTAS-INFORMATICA |

### COMANDOS TOPOLOGIA 2

##### etherchannel

####### ESW1

conf t
int range f1/0 -2
channel-group 2 mode on
end

conf t
int range f1/3 -5
channel-group 3 mode on
end

conf t
int range f1/6 -7
channel-group 1 mode on
end

####### ESW2

conf t
int range f1/0 -2
channel-group 5 mode on
end

conf t
int range f1/3 -5
channel-group 4 mode on
end

conf t
int range f1/6 -7
channel-group 1 mode on
end

####### ESW3

conf t
int range f1/0 -2
channel-group 2 mode on
end

conf t
int range f1/3 -5
channel-group 4 mode on
end

####### ESW4

conf t
int range f1/0 -2
channel-group 5 mode on
end

conf t
int range f1/3 -5
channel-group 3 mode on
end

##### vtp

####### ESW1
conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode server
end

####### ESW2
conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end

####### ESW3
conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end

####### ESW4
conf t
vtp domain Grupo5
vtp password Grupo5
vtp mode client
end

##### VLAN

####### ESW1
conf t

vlan 10
name ADMINISTRACION
exit

vlan 20
name CONTABILIDAD
exit

vlan 30
name VENTAS-INFORMATICA
end

##### TRUNK

####### ESW1
conf t
int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit
end

int f1/8
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit
end

####### ESW2
conf t
int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit
end

####### ESW3
conf t

int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int f1/6
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

end

####### ESW4
conf t

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

int Po5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit

end


##### STP
####### ESW1
conf t
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root primary
spanning-tree vlan 30 root primary
end

sh spanning-tree root
