Template criado para monitorar o Uso de Memória RAM feito pelo ARC do ZFS em ambiente Proxmox.  

Telegram: @erickandrade  
Blog: https://erickandrade.com.br  
E-mail: erick[@]erickandrade.com.br  

Zabbix Server: 6.0.29  
Zabbix Agent: 6.0.3

# Instrução de Instalação e Uso

Monitorando uso do ARC ZFS no Zabbix

Esse monitoramento foi criado por uma necessidade especifica dentro do ambiente Proxmox. O uso do ARC foi definido nas configuracoes mas mesmo assim se faz necessario saber seu uso real.

1 - Crie um arquivo chamado uso_ram_zfs.conf dentro do diretorio /etc/zabbix/zabbix_agentd.conf.d/.

touch /etc/zabbix/zabbix_agentd.conf.d/uso_ram_zfs.conf

2 - Edite o arquivo e coloque a linha do UserParameter nele.

nano /etc/zabbix/zabbix_agentd.conf.d/uso_ram_zfs.conf

UserParameter=system.zfs.mempct,awk '/^size/ { printf "%.2f\n", $3 / 1048576 }' < /proc/spl/kstat/zfs/arcstats

3 - Baixe o template criado por mim no meu Github para importar ou crie um item dentro do seu host.

Parâmetros:

Nome: Uso de RAM ZFS  
Tipo: Agente Zabbix  
Chave: system.zfs.mempct  
Tipo de informação: Numérico (fracionário)  
Unidade: M  
