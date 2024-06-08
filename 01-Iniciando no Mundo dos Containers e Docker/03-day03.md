# Day 03:



## Exame Teórico:

### 01 - O que é Trivy?
É um scanner de vulnerabilidades de container.

### 02 - O que ele é capaz de realizar?
Trivy é capaz de detectar vulnerabilidades de SO e de aplicativos.

### 03 - Como o Trivy é normalmente usado no ciclo de vida do desenvolvimento de software? 
Para scanner de vulnerabilidades no processo de CI/CD.

### 04 - Por que é importante ter imagens de contêiner menores?
RPara reduzir o tempo de deploy e minimizar o espaço de armazenamento necessário.

### 05 - Como ter menos camadas em uma imagem de container pode beneficiar a segurança?
Menos camadas tornam mais difícil para os atacantes explorarem vulnerabilidades. Menos camadas resultam em menos componentes para gerenciar e potencialmente atualizar. Menos camadas reduzem o tamanho da imagem do container.

### 06 - Por que é aconselhável ter menos pacotes em uma imagem de container?
Isso reduz o número de possíveis pontos de falha. Aumenta a velocidade de inicialização do container. Isso faz com que seja mais fácil de implementar a imagem.

### 07 - Qual é a relação entre o número de pacotes em uma imagem de contêiner e o número de vulnerabilidades potenciais?
Mais pacotes geralmente levam a mais vulnerabilidades potenciais.

### 08 - Como as imagens distroless ajudam a minimizar as vulnerabilidades?
Elas contêm apenas as dependências necessárias, reduzindo a superfície de ataque. Elas são menores em tamanho, tornando-as mais rápidas para implantar. Elas são mais fáceis de gerenciar devido ao número reduzido de componentes
