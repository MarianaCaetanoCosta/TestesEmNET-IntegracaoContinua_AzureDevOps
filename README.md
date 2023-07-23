# Testes em .NET - Integração Continua com AzureDevOps

 Testes em .NET: integração e entrega contínua com Azure DevOps

# 01. DevOps

### Apresentação

O Projeto é o Alura ByteBank, uma solução .NET composta por 5 projetos: projeto de domínio; de aplicação; de infraestrutura, que vai configurar e conectar com o banco de dados MySQL; de apresentação, que terá a apresentação web que vamos hospedar na nuvem; e o projeto de teste, que contém três projetos de domínio, de infraestrutura e também o de integração de interface.

O Alura ByteBank é a solução que permite trabalhar com contas bancárias, cadastrar contas, clientes, agências.

### Preparando o ambiente

[Visual Studio Community](https://visualstudio.microsoft.com/pt-br/free-developer-offers/)

[GitHub](https://github.com/alura-cursos/Alura.ByteBank.WebApp)

Abrindo nossa solução “Alura.ByteBank”, vá até o gerenciador de soluções no lado direito e verifique a estrutura de pastas de projeto que deve conter:

![alt text: Tela do MS Visual Studio Community para o projeto Alura.ByteBank</code></code></code></code>. Vemos as pastas “Dominio”, “Aplicacao”, “Infraestrutura” e “Testes” ](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem1.png)

Com o projeto de dados aberto, vamos verificar e instalar as dependências do Entity Framework e Pomelo (provedor de acesso ao banco de dados do MySQL, ferramenta que vai possibilitar o projeto se comunicar com o banco do MySQL).

![alt text: Na imagem é apresentado um recorte do gerenciador de soluções do Visual Studio, no projeto de dados e apresentando os pacotes de instalação necessários: EntityFramework Core e Pomelo.](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem2.png)

[MySQL Community Downloads](https://dev.mysql.com/downloads)

Na página oficial da ferramenta [MySQL Community Downloads](https://dev.mysql.com/downloads) selecione a opção de download. Trabalhamos com a versão para Windows:

![alt text: Na imagem vemos a página de download da ferramenta MySQL Community](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem3.png)

Execute o instalador após o término do download e selecione “Developer Default”, que traz como opção a instalação do MySQL Workbench também.

![alt text: Na imagem vemos a tela do instalador Windows do MySQL Community com a opção “Developer Default” selecionada.](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem4.png)

Proceda a instalação dos componentes clicando no botão ”Execute”, como mostrado na imagem:

![alt text: Na imagem é apresentada a tela do instalador Windows do MySQL Community, mostrando os componentes que serão instalados, incluindo o MySQL e MySQL Worbench.](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem5.png)

Durante o processo de instalação devemos prestar atenção à configuração da senha de acesso ao serviço de banco de dados do MySQL, já que na criação da string de conexão nós vamos utilizar essa informação.

Com as ferramentas instaladas, acesse o MySQL Workbench e crie um schema `bytebankbd`, como na imagem abaixo:

![alt text: Na imagem é apresentado a tela do instalador MySQL Worbench com o schema bytebankbd</code></code></code></code> criado. ](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem6.png)

Abrindo a nossa solução “Alura.ByteBank”, vá até a classe `ByteBankContexto` no projeto e configure a string de conexão no método `OnConfiguring`.

![alt text: Tela do MS Visual Studio Community, para o projeto Alura.ByteBank.Dados</code></code></code></code> com a classe ByteBankContexto</code></code></code></code> exibindo a string de conexão no método OnConfiguring</code></code></code></code>. ](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem7.png)

Para configurar o banco de dados, devemos executar todas as migrações da pasta “Migrations” executando o comando `dotnet ef database update`.

![alt text: Na imagem é apresentado um recorte do gerenciador de soluções do visual studio. As migrações devem ser executadas no projeto de dados.](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem8.png)

Após a execução, abrir a ferramenta de gestão da base de dados MySQL Workbench e verificar se as tabelas foram criadas e os dados inseridos corretamente.

![alt text: Na imagem é apresentado um recorte do MySQL WorkBench mostrando as tabelas do banco de dados.](https://caelum-online-public.s3.amazonaws.com/2407-testes-net-integracao-entrega-continua-azure-devops/01/aula1-imagem9.png)

Agora já podemos começar!

### Criando uma conta no Azure

[Azure](azure.microsoft.com/pt-br)

### Para saber mais: o que é Cloud Computing e seus benefícios?

*Cloud Computing* ou simplesmente  **Computação em Nuvem** , é um conjunto de tecnologias que permite o acesso a softwares de armazenamento ou processamento através da internet. Isso traz o benefício de acessar essas ferramentas por meio de aparelhos como um smartphone ou qualquer computador com conexão com a internet.

Como exemplos usuais temos os webmails (Google, Yahoo, Outlook), ferramentas de armazenamento como Google Drive, DropBox e OneDrive e ferramentas de escritórios como o Office 360.

Por meio de empresas como Google, Microsoft ou Amazon, hoje a “nuvem” já consegue disponibilizar uma série de softwares que atendem a empresas de desenvolvimento fornecendo hospedagem e gerenciamento de aplicações, implementações de servidores de serviço, banco de dados e processamento de imagens. E não é necessário ter nenhum desses serviços instalados na infraestrutura.

### DevOps e Azure DevOps

Etapas

Plano -> Código -> Integração -> Teste -> Release -> Deploy -> Operação

Plano

Precisamos ter um plano, uma ideia do que é preciso ser feito, do que o cliente precisa. Para atender o cliente, qual linguagem eu vou utilizar? Qual infraestrutura? Qual banco de dados? Vai ser hospedado na nuvem? Minha solução vai rodar no ambiente interno da empresa? Então essa parte é importante – iniciar todo esse processo.

Código

Quais algoritmos eu vou implementar, quais boas práticas, quais padrões de projetos. À medida que eu for codificando, eu vou integrando.

Por exemplo: desenvolvi um módulo de cadastro de cliente, esse módulo faz referência ao “Contas a pagar e receber” da minha solução e, à medida que eu vou codificando e integrando esses módulos, eu vou testando.

Teste

Vou testar a codificação do que foi feito, porque eu preciso ter certeza, na medida do possível, de que as novas funcionalidades que estou integrando na minha solução não vão parar o que é estava funcionando.

Feito isso: codifiquei, integrei e testei, vou liberar uma  *release* , um código funcional que o meu cliente/usuário pode testar para validar se está certo, se está atendendo ao plano definido no início do processo.

Deploy

Está tudo certo? Então, vou fazer o *deploy* da aplicação, vou implantar a aplicação no ambiente. Vou instalar no servidor, para ser usado na intranet da empresa, ou vou pegar essa solução e implantar numa plataforma de nuvem, no  *cloud* , por exemplo.

Papeis de Operações

* Manter a solução em funcionamento para cliente
* Infraestrutura

Então o que é DevOps?

* Dev + Ops
* Integração

Integração da equipe de desenvolvimento com a equipe de operações para manter o software funcionando desde a criação concepção do software até a entrega no ambiente de produção do usuário.

Isso é muito importante porque vai permitir a entrega de um produto com maior valor, com maior qualidade, isso é perceptivel para o nosso cliente a partir dos processos, da integração cada vez maior dessas duas equipes.

O Azure DevOps, que é uma ferramenta do ambiente da Microsoft. Mas DevOps não é só ferramenta, é um conjunto de cultura, de processos, de rotinas, de documentação, e todo esse cenário, todos esses ícones, vão fazendo com que o DevOps funcione da maneira adequada.

### DevOps

David foi recém-contratado como desenvolvedor Júnior em uma empresa. Ele chegou à equipe com a responsabilidade de ajudar na criação e implementação do DevOps na organização, alinhando processos, definindo ferramentas além de disseminar a cultura DevOps em toda a organização, que neste ano inicia o projeto corporativo de implantação de processos ágeis.

A respeito do DevOps, marque as alternativas corretas.

Selecione 2 alternativas*  [ ] O DevOps é uma metodologia focada em reunir diferentes processos dentro do desenvolvimento de uma aplicação e executá-los de maneira sistematizada.

* Alternativa correta
  [ ] O DevOps é uma metodologia focada em reunir diferentes processos dentro do desenvolvimento de uma aplicação e executá-los de maneira sistematizada.

  Alternativa incorreta. DevOps vai além de simplesmente automatizar tarefas.
* Alternativa correta
  [ ] Na implementação de uma cultura DevOps. David deve propor a adoção de uma documentação técnica extensa, sobretudo em relação às ferramentas que vão implementar DevOps.

  Alternativa incorreta. DevOps parte da adoção do método ágil, focado em entregar valor para o cliente documentando o que for necessário.
* Alternativa correta
  [X] David deverá trabalhar em sintonia com a equipe de operações. Por meio de um trabalho colaborativo, devem conseguir implantar testes automatizados e automação de fluxos referentes à infraestrutura.

  Alternativa correta. DevOps pressupõe uma forte colaboração entre a equipe de desenvolvimento e operação para a criação de um ambiente ágil com foco em resultados e menos conflitos.
* Alternativa correta
  [X] Na implementação de DevOps pela empresa, David percebe que suas atividades não se resumem a automação de processos e adoção de ferramentas.

  Alternativa correta. DevOps vai muito além da automação e uso de ferramentas, envolve a adoção de uma cultura ágil de integração do desenvolvimento com a operação, com objetivo de um melhor resultado.

### O que aprendemos?

* Para criar uma conta no Azure e vinculá-la ao Azure DevOps, precisamos primeiramente criar uma conta na Microsoft;

* A plataforma de nuvem que utilizaremos para hospedar a aplicação do ByteBank será a Azure;
* Por meio do Azure Devops teremos suporte para a implementação de integração e entrega contínua da aplicação, de forma automatizada;
* DevOps é a integração cada vez maior da equipe de desenvolvimento e operações, criando uma cultura com o intuito de entregar uma solução de software com mais valor e qualidade, otimizando processos e automatizando rotinas.

# 02. Versionando o código

Gerenciamento de código
