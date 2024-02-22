# windows-hyper-v-como-configurar-a-replica-o-de--vms--maquinas-virtuais-usando-o-hyper-v-core
## Script de Instalação do GLPI

### Video Referencia:

[Como configurar a Replicação de "VMs" Maquinas Virtuais usando o Hyper-V Core  | MasterMindTI](https://youtu.be/_OjuhFMcXfA)

## Vamos para o Script ?
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" width="40" height="40"/> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="40" height="40"/> <img src="https://raw.githubusercontent.com/glpi-project/glpi/master/pics/logos/logo-GLPI-250-black.png" width="60" height="60"/>
                

####################################################################
## . Pré-Requisitos
####################################################################
- 2 Servidores Hyperv Core 2019 instalados
- Acesso a internet para baixar o script e os pacotes
- Acesso de Administrador

############################# PASSO 1 ################################
### CRIAR A UNIDADE CERTIFICADORA E AUTOASSINAR O CERTIFICADO RAIZ ###
######################################################################

### SERVIDOR 1
- 1.1. Comandos
```
makecert -pe -n "CN=MS01CA" -ss root -sr LocalMachine -sky signature -r "MS01CA.cer"
makecert -pe -n "CN=MS01" -ss my -sr LocalMachine -sky exchange -eku 1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2 -in "MS01CA" -is root -ir LocalMachine -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 MS01Cert.cer
```

### SERVIDOR 2
- 1.2. Comandos

```
makecert -pe -n "CN=MS02CA" -ss root -sr LocalMachine -sky signature -r "MS02CA.cer"
makecert -pe -n "CN=MS02" -ss my -sr LocalMachine -sky exchange -eku 1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2 -in "MS02CA" -is root -ir LocalMachine -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 MS02Cert.cer
```

################### PASSO 2 #####################
### IMPORTANDO OS CERTIFICADOS NOS SERVIDORES ###
#################################################

- 2.1. NO SERVIDOR 1 (MS01) COPIAR OS CERTIFICADOS DOS SERVIDORES 2 E IMPORTAR

```
certutil -addstore -f Root "MS02CA.cer"
```

- 2.2. NO SERVIDOR 2 (MS02) COPIAR OS CERTIFICADOS DOS SERVIDORES 1 E IMPORTAR

```
certutil -addstore -f Root "MS01CA.cer"
```

############### PASSO 3 ###############
### ALTERAR O REGISTRO E REINICIAR ###
#######################################

- 3.1.

```
reg add “HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\Replication” /v DisableCertRevocationCheck /d 1 /t REG_DWORD /f
```

####################################################################
## Informações Adicionais:
#### MasterMindTI - Como configurar a Replicação de "VMs" Maquinas Virtuais usando o Hyper-V Core
#### Procedimento: windows-hyper-v-como-configurar-a-replica-o-de--vms--maquinas-virtuais-usando-o-hyper-v-core
#### @Responsável: Miller Santos
#### @Data: 22/02/2024
#### @Versão: 1.0.0
#### @Homologado: Hyperv Core em Windows Server 2019
####################################################################

### Video Referencia:

[Como configurar a Replicação de "VMs" Maquinas Virtuais usando o Hyper-V Core  | MasterMindTI](https://youtu.be/_OjuhFMcXfA)

### Qualquer dúvida, entre em contato.

e-mail: contato@mastermindti.com.br

## Contatos:

<div>
<a href="https://www.youtube.com/@mastermindti" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
<a href = "mailto:contato@mastermindti.com.br"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
<a href="https://www.linkedin.com/in/miller-guilherme-santos-42046471/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a>   
</div>

## Estatisticas

<div>
<a href="https://github.com/MasterMindTI">
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=MasterMindTI&show_icons=true&theme=dracula&include_all_commits=true&count_private=true"/>
</div>

