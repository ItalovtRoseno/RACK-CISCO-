São Paulo, may 24 2022

    Inicio da Nanobyte

!Teste de link permanente 
Ponto 6 - Wesley OK (PC para OUT OF BAND)
Ponto 7 - Italo OK
Ponto 8 - Murilo OK

!RESET DO SWITCH Layer 3 3560 (de 1000 a 2000)


    Utilizando RJ42 & DB9, para conexão fora de Banda (OUT OF BAND)
    Acessar software PuTTy 
    
                serial line: COM1
                Connection type: serial
                Speed: 9600

!reset do switch 

    Pressionar botão MODE no switch cerca de 20 a 30 segundos, até que apareça uma mensagem de RESET
    - Se aparecer "deseja utilizar wizzard para configurar o switch, pressionar NÃO".

!RESET do Router
Desligar e ligar o router, e assim que ele estiver iniciando e aparecer os sustenidos clicar com o botão direito na barra superior do putty special>>> break (rapido)

!configuraçao do router
confreg 0x2142 (ele impede de ler o startup config para iniciar)
reset (para iniciar confreg novo) 
depois escreva no 

!limpando as configuraçaoes do router
entrar um modo privelegiado enable
erase startup-config
configure terminal 
config-register 0x2102 (voltar a ler o startup)
ctrl+z para descer tudo 
copy rounning-config startup-config (salvando a nova configuraçao no startup)
reload 
esperar router iniciar

enable 
show version 
ver se a configuração de registro esta certo!(configuration register is 0x2102).

!!!ConfiguraçãoDoSVIDoSwitch!!


enable 

configure terminal 

!configuraçao de gatewai padrao ipv4 do svi 

ip default-gateway 172.16.20.254

!!configuraçao da interface virtual VLAN SVI 

interface vlan 20 

!configuraçao de descriçao 
description interface SIV de gerenciamento do grupo-02

ip address 172.16.20.253 255.255.255.0

inicializar a interface 

no shutdown 

end 

copy running-config
show ip interface brief
show vlan brief 
show vlan id????

!!Configuração Da Interface Do Roteador!!

enable 

configure terminal 

interface gigabitEthernet 0/0.20

no shutdown 

exit

interface gigabitEthernet 0/0.20

description subinterface da vlan de SVI do switch layer 3 3560

encapsulation dot1Q 20

ip address 172.16.20.254 255.255.255.0

exit

interface gigabitEthernet 0/0.21 

description subinterface da vlan murilo

encapsulation dot1Q 21

ip address 172.16.21.254 255.255.255.0

exit 

interface gigabitEthernet 0/0.22

description subinterface da vlan italo

encapsulation dot1Q 22

ip address 172.16.22.254 255.255.255.0

exit 

interface gigabitEthernet 0/0.23

description subinterface da vlan wesley 

encapsulation dot1Q 23

ip address 172.16.23.254 255.255.255.0

exit 

interface gigabitEthernet 0/0.25

description subinterface da vlan Wifi 

encapsulation dot1Q 25

ip address 172.16.25.254 255.255.255.0

exit 

ConfiguraçãoDoDHCP-Server No Router

enable

connfigure terminal 

!!configurando o pool do DHCP server da vlan do primeiro usuario!!!!!!!!

ip dhcp excluded-address 172.16.21.1 172.16.21.100
ip dhcp ecluded-address 172.16.21.1 172.16.21.254
ip dhcp pool vlan-21
network 172.16.21.0 255.255.255.0
default-router 172.16.21.254
dsn-server 8.8.8.8 8.8.4.4
domain-name senac.br
exit

ip dhcp excluded-address 172.16.21.1 172.16.21.100
ip dhcp excluded-address 172.16.22.1 172.16.22.254
ip dhcp pool vlan-22
network 172.16.22.0 255.255.255.0
default-router 172.16.22.254
dsn-server 8.8.8.8 8.8.4.4
domain-name senac.br
exit


ip dhcp excluded-address 172.16.21.1 172.16.23.100
ip dhcp excluded-address 172.16.21.1 172.16.23.254
ip dhcp pool vlan-23
network 172.16.23.0 255.255.255.0
default-router 172.16.23.254
dsn-server 8.8.8.8 8.8.4.4
domain-name senac.br
exit


!salvando as configuraçoes 
copy  running-config startup-config

verificando as informaçoes do pool DHCP server 

show ip dhcp pool 
show ip dhcp binding 



