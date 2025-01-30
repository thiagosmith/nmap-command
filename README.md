# nmap-command
Comandos executados do nmap

# POrtas e Serviços
$ sort -t$'\t' -k3 -n -r /usr/share/nmap/nmap-services | less

$ sort -t$'\t' -k3 -n -r /usr/share/nmap/nmap-services > ports.txt

$ cat ports.txt | grep -v udp | head -n10

$ cat ports.txt | grep -v tcp | head -n10

$ cat /etc/services

$ cat /etc/services | grep ftp
 
$ cat /etc/services | grep http

$ cat /etc/services | grep ssh



# OPÇÔES:
$ nmap -h



# HOST DISCOVERY:
$ ip -br a

$ nmap -sn 192.168.90.0/24

$ nmap -sn 192.168.90.0/24 -oG hosts.txt

$ cat hosts.txt

$ cat hosts.txt | grep "Host"

$ cat hosts.txt | grep "Host" | cut -d " " -f2 

$ cat hosts.txt | grep "Host" | cut -d " " -f2 > alvos.txt

$ cat alvos.txt



# Forçar a varredura sem fazer o ping

$ nmap 192.168.90.151

$ nmap 192.168.90.151 -Pn



# SCAN TECHNIQUES:

$ nmap -sS 192.168.90.9

$ nmap -sT 192.168.90.9

$ nmap -sU 192.168.90.9

$ nmap -sU 192.168.90.9 --top-ports=10

$ nmap -sU 192.168.90.9 --top-ports=10 --open



# PORT SPECIFICATION AND SCAN ORDER:

$ nmap 192.168.90.9 -p21 

$ nmap 192.168.90.9 -p21-25,80,445

$ nmap 192.168.90.9 -p21-25,80,445 –exclude-ports=22

$ nmap 192.168.90.9 -r

$ nmap 192.168.90.9 --top-ports=100



# SERVICE/VERSION DETECTION:

$ nmap 192.168.90.9 -p21 -sV

$ nmap 192.168.90.9 -sC

$ nmap 192.168.90.9 -O



# SCAN BÁSICO

$ nmap 192.168.90.9 -v

$ nmap 192.168.90.9 -vv

$ nmap 192.168.90.9 -v -sV

$ nmap 192.168.90.9 -v -T4 

$ nmap 192.168.90.9 -v -T1

$ nmap 192.168.90.9 -v -p 22,80,443

$ nmap 192.168.90.9 -v -p- 

$ nmap 192.168.90.9 -v -p- --min-rate=5000

$ nmap 192.168.90.9 -v -A

$ nmap 192.168.90.9 -v -sC

$ nmap -sV -6 fe80::a00:27ff:fede:c7af

$ nmap -sV -6 fe80::a00:27ff:fede:c7af -p-

$ nmap 192.168.90.9 --traceroute



# TÉCNICAS DE EVASÃO

$ nmap -f 192.168.90.9

$ nmap 192.168.90.9 --scan-delay=500ms

$ nmap 192.168.90.9 -D RND:10

$ nmap 192.168.90.9 -D 192.168.0.1,192.168.1.1-9

$ nmap 192.168.90.9 -D 192.168.0.1,ME,.168.0.3

$ nmap 192.168.90.9 -g53,80,443



# SCRIPTS: Localização / Help

$ ls /usr/share/nmap/scripts/

$ ls /usr/share/nmap/scripts/smb*

$ ls /usr/share/nmap/scripts/ftp*

$ grep categories /usr/share/nmap/scripts/* | grep exploit

(vuln, auth, brute, default, discovery, malware, safe, version)



$ nmap --script-help=ftp-anon



# CATEGORIAS DE SCRIPTS

$ nmap 192.168.90.9 -sV -v -p- --script=vuln

$ nmap 192.168.90.9 -sV -v -p- --script=auth

$ nmap 192.168.90.9 -sV -v -p- --script=brute

$ nmap 192.168.90.9 -sV -v -p- --script=default

$ nmap 192.168.90.9 -sV -v -p- --script=discovery

$ nmap 192.168.90.9 -sV -v -p- --script=exploit

$ nmap 192.168.90.9 -sV -v -p- --script=malware

$ nmap 192.168.90.9 -sV -v -p- --script=safe

$ nmap 192.168.90.9 -sV -v -p- --script=version



# EXECUÇÃO DE SCRIPTS INDIVIDUALIZADOS

$ nmap 192.168.90.9 -sV -v -p2121 --script=ftp-brute 

$ nmap 192.168.90.9 -sV -v -p2121 --script=ftp-brute --script-args userdb=user.txt,passdb=pass.txt

$ nmap 192.168.90.9 -sV -v -p22 --script=ssh-run --script-args "username=msfadmin,password=msfadmin,cmd='ls -la'"

$ nmap 192.168.90.9 -sV -v -p21 --script=ftp-vsftpd-backdoor

$ nmap 192.168.90.9 -sV -v -p21 --script=ftp-vsftpd-backdoor --script-args="ftp-vsftpd-backdoor.cmd='ls -la /'"

$ nmap 192.168.90.9 -sV -p80 --script=http-title,http-server-header,http-headers,http-methods,http-enum,http-brute

$ nmap 192.168.90.9 -sV -p111 --script=rpcinfo

$ nmap 192.168.90.9 -sV -p1099 --script=rmi-vuln-classloader

$ nmap 192.168.90.9 -sV -p3306 --script=mysql-*

$ nmap 192.168.90.9 -sV -p3632 --script=distcc-cve2004-2687

$ nmap 192.168.90.9 -sV -p3632 --script=distcc-cve2004-2687 --script-args="distcc-cve2004-2687.cmd='ls -lha'"

$ nmap 192.168.90.9 -sV -p80 --script=http-enum --script-args http.useragent="Seu-User-Agent"
