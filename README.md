# Atividade_Aws_Linux_Compass
## Requisitos AWS: 
Gerar uma chave pública para acesso ao ambiente; Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Família t3.small, 16 GB SSD); Gerar 1 elastic IP e anexar à instância EC2; Liberar as portas de comunicação para acesso público: (22/TCP, 111/TCP e UDP, 2049/TCP/UDP, 80/TCP, 443/TCP).

## Requisitos no linux: 
Configurar o NFS entregue;

Criar um diretório dentro do filesystem do NFS com seu nome; 

Subir um apache no servidor - o apache deve estar online e rodando; 

Criar um script que valide se o serviço está online e envie o resultado da validação para o seu diretório no nfs; 

O script deve conter - Data HORA + nome do serviço + Status + mensagem personalizada de ONLINE ou offline;

O script deve gerar 2 arquivos de saida: 1 para o serviço online e 1 para o serviço OFFLINE; 

Preparar a execução automatizada do script a cada 5 minutos.

## Instruções de Execução da Atividade
## AWS >> Geração de chave pública
* Acessar a AWS na página do serviço EC2, e clicar em "Pares de chaves" no menu lateral esquerdo.
* Clicar em "Criar par de chaves".
* A tela de criação será aberta e nela você poderá escolher um nome para o par de chaves.

 ![Texto Alternativo](https://github.com/oliamanda/Atividade_Aws_Linux_Compass/blob/main/cria%C3%A7%C3%A3o_par_de_chaves.png?raw=true)

 # AWS >> Criação de uma VPC
* Acessar a AWS na página do serviço VPC, e clicar em "Criar VPC";
* Atribua um nome a sua VPC;
* Especifique um bloco CIDR IPv4 para sua VPC;
* Feito isso, basta clicar em Criar VPC.
  
 ![Texto Alternativo](https://raw.githubusercontent.com/oliamanda/Atividade_Aws_Linux_Compass/2b8145b9410422deb337921fd425ceeb9b984bd8/cria%C3%A7%C3%A3o_vpc.png)


* # AWS >> Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Família t3.small, 16 GB SSD) 
* No Painel EC2 no console AWS, clique em Instâncias no menu ao lado esquerdo da tela e clique em “Executar instância”;
* Configurar as Tags da instância (Name, Project e CostCenter) para instâncias e volumes;
* Selecionar a imagem Amazon Linux 2 AMI (HVM), SSD Volume Type.
* Selecionar o tipo de instância t3.small.
* Selecionar a chave gerada anteriormente.
* Em configurações de Rede, selecione a opção Criar Grupo de segurança;
* Ainda nessa seção, deixe marcada a opção Permitir tráfego SSH de Qualquer Lugar (0.0.0.0/0);
* Colocar 16 GB de armazenamento gp2 (SSD).
* Clicar em "Executar instância".
* Revise se as configurações estão de acordo com as recomendações dos instrutores e clique em “Executar Instância”.

 ![Texto Alternativo](https://github.com/oliamanda/Atividade_Aws_Linux_Compass/blob/main/ec2_.png?raw=true)

  
# AWS >> Criando Gateway de Internet
* No console da AWS acesse a página do serviço VPC, e clique em "Gateways de internet" no menu lateral esquerdo.
* Clicar em "Criar gateway de internet".
* Definir um nome para o gateway e clicar em "Criar gateway de internet".
* Selecionar o gateway criado e clicar em "Ações" > "Associar à VPC".
* Selecionar a VPC da instância EC2 criada anteriormente e clicar em "Associar".


# AWS >>Alocar um endereço IP elástico e anexar a instância EC2.
* Acessar a AWS na pagina do serviço EC2, e clicar em "IPs elásticos" no menu lateral esquerdo.
* Clicar em "Alocar endereço IP elástico".
* Selecionar o ip alocado e clicar em "Ações" > "Associar endereço IP elástico".
* Selecionar a instância EC2 criada anteriormente;
* Marque a opção “Permitir que o endereço IP elástico seja reassociado”;
* Clicar em "Associar".


# AWS >> Liberar as portas de comunicação para acesso público
* No console da AWS na página do serviço EC2,  clique em "Segurança" > "Grupos de segurança" no menu lateral esquerdo.
* Selecionar o grupo de segurança da instância EC2 criada anteriormente.
* Clicar em "Editar regras de entrada".
* A regra de entrada, do Tipo SSH, no Intervalo de portas 22, Protocolo TCP já  vem com uma configuração padrão, então vamos manter essa regra e adicionar apenas as demais regras exigidas pelos orientadores, conforme o exemplo abaixo.

![Texto Alternativo](https://github.com/oliamanda/Atividade_Aws_Linux_Compass/blob/main/portas_de_comunica%C3%A7%C3%A3o.png?raw=true)


# AWS >> Configurar rota de internet 
* No console da AWS na página do serviço VPC, e clique em "Tabelas de rotas" no menu lateral esquerdo.
* Selecionar a tabela de rotas da VPC da instância EC2 criada anteriormente.
* Clicar em "Ações" > "Editar rotas".
* Clicar em "Adicionar rota".
* Configurar da seguinte forma:
* Destino: 0.0.0.0/0
* Alvo: Selecionar o gateway de internet criado anteriormente
* Clicar em "Salvar alterações".


# Linux >> Configuração do NFS com o IP fornecido
* Criar um novo diretório para o NFS usando o comando sudo mkdir /mnt/nfs.
* Montar o NFS no diretório criado usando o comando sudo mount IP_OU_DNS_DO_NFS:/ /mnt/nfs.
* Verificar se o NFS foi montado usando o comando df -h.
* Configurar o NFS para montar automaticamente no boot usando o comando sudo nano /etc/fstab.
* Adicionar a seguinte linha de comando no arquivo /etc/fstab:
* Ex: IP_OU_DNS_DO_NFS:/ /mnt/nfs nfs defaults 0 0
* Salvar o arquivo /etc/fstab.
* Criar um novo diretório para o usuário com seu nome;
Ex: usando o comando sudo mkdir /mnt/nfs/amandaoliveira


# Linux >> Configuração do Apache.
## EXECUTE OS SEGUINTES COMANDOS ABAIXO:
* Executar o comando sudo yum update -y para atualizar o sistema.
* Executar o comando sudo yum install httpd -y para instalar o apache.
* Executar o comando sudo systemctl start httpd para iniciar o apache.
* Executar o comando sudo systemctl enable httpd para habilitar o apache para iniciar automaticamente.
* Executar o comando sudo systemctl status httpd para verificar o status do apache.


  # Linux >> Configurar o script de validação.
## RECOMENDAÇÕES: 
### O script deve conter - Data HORA + nome do serviço + Status + mensagem personalizada de ONLINE ou offline;
### O script deve gerar 2 arquivos de saída: 1 para o serviço online e 1 para o serviço OFFLINE;

* Crie um novo arquivo de script usando o comando "nano script.sh".
* Adicione as seguintes linhas de código no arquivo de script:

![Texto Alternativo](https://github.com/oliamanda/Atividade_Aws_Linux_Compass/blob/main/script.png?raw=true)

* Salve o arquivo de script usando ctrl+x > y > enter
* Execute o comando chmod +x script.sh para tornar o arquivo de script executável.
* Execute o comando  ./script.sh para executar o script.
* Salve o arquivo de cronjob usando ctrl+x > y > enter
* Execute o comando crontab -l para verificar se o cronjob foi configurado corretamente


# Linux >> Configuração da execução do script de validação a cada 5 minutos.
* Execute o comando  EDITOR=nano crontab -e  para editar o cronjob.
* Adicione a seguinte linha de código no arquivo de cronjob:
* */5 * * * * /home/ec2-user/script.sh

 # Referências 📚
## Documentação oficial Amazon AWS fornecidas nas aulas: https://docs.aws.amazon.com/pt_br/

  

