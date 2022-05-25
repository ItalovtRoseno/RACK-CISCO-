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



