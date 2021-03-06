# TCPDUMP

Monitorar o adaptador de rede eth0:  
```bash
tcpdump -v -i eth0 # -v (modo verbose), -i (Interface)
```

Monitorar o adaptador de rede e salvar em um arquivo:  
```bash
tcpdump -v -i eth0 -w scanner.pcap
```

Monitorar apenas o protocolo icmp:  
```bash
tcpdump -v -i etho icmp -w scanner_icmp.pcap
```

Abrir um arquivo de monitoramento em formato PCAP:  
```bash
tcpdump -v -r scanner_icmp.pcap # -r (ler um arquivo)
```

Mostrar IP ao invés do nome do host:  
```bash
tcpdump -vnr scanner_icmp.pcap # -n (mostra o IP)
```

Filtrando por protocolos UDP:  
```bash
tcpdump -vnr scanner.pcap udp
```

Filtrando por protocolos TCP:  
```bash
tcpdump -vnr scanner.pcap tcpdump
```

Filtrando por IP:  
```bash
tcpdump -vnr scanner.pcap host 192.168.0.200
```

Filtrando por IP entre dois endereços:  
```bash
tcpdump -vnr scanner.pcap host 192.168.0.200 and 192.168.0.1
```

Filtrando por IP de origem e destino:  
```bash
tcpdump -vnr scanner.pcap src host 192.168.0.200 and dst 192.168.0.1
```

Filtrando por porta:  
```bash
tcpdump -vnr scanner.pcap port 21
```

Visualiza os caracteres em ASCII nos pacotes:  
```bash
tcpdump -vnAr scanner.pcap port 21
```

Visualiza os caracteres em Hexadecimal nos pacotes:  
```bash
tcpdump -vnXr scanner.pcap port 21
```

Pesquisa por string nos pacotes:  
```bash
tcpdump -vnAr scanner.pcap port 21 | grep "pass"
```
```bash
tcpdump -vnXr scanner.pcap port 21 | grep "pass"
```

Verificar os IPs envolvidos:  
```bash
tcpdump -vnr scanner.pcap | cut -d " " -f5 | grep -v "ttl" | sort -u
```

Filtrando de forma tratada o IP de origem:  
```bash
tcpdump -vnr scanner.pcap src host 192.168.0.200 | cut -d "," -f1 | grep -v "tos"
```
*Flags: [S] ==> Sync, [F] ==> Finish, [R] ==> Reset, [.] ==> ACK*  
*Sempre quando há uma flag de "finish" significa que foi estabelecido a conexão.*

Filtrando de forma tratada o IP de origem e as conexões finalizadas:  
```bash
tcpdump -vnr scanner.pcap src host 192.168.0.200 | cut -d "," -f1 | grep -v "tos" | grep -v "[S]" | grep "F\."
```
