# RPE-Answers

### Arquitetura de Front-end (coloquei nos arquivos uma imagem de como seria a arquitetura que imaginei para uma aplicação dessa forma `PATH da image: src -> assets -> file`):

- Como primeiro passo sendo a escolha das tecnologias para serem utilizadas no projeto. A escolha consistiria em:
  * Biblioteca Front-end: React
    * A escolha do React em geral vem da popularidade dele com uma comunidade de devs grande, fazendo assim com que suporte, bibliotecas complementares e até numa futura procura por nova contratação para agregar com o time.
    * Em questão de perfomance, mesmo para aplicações grandes e complexas o React perfoma bem dada a utilização de renderização seletiva e virtual DOM.
    * Uma outra vantagem seria a componentização de toda a estrutura do frontend. Fazendo assim com que se tenha um código bastante modularizado e reutilizável.
  * Biblioteca de Estilização sendo Styled-Components ou Tailwind
    * Styled-Components sendo uma biblioteca de css in js, permite que seja escrito uma forma de estilo encapsulado e modular, o que facilita numa futura necessidade de manutenção de código.
    * Tailwind é uma alternativa para processos mais rápidos de desenvolvimento dada que a escrita é feita em forma de classe no mesmo arquivo.
    * Ambas as bibliotecas servem para a finalidade de construir uma aplicação escalável e a barreira de aprendizado é mínima, então para o caso de um futuro desenvolvedor ter que dar manutenção no código seria mais fácil.
  * State Management com Redux usando Redux Toolkit
    * O Redux possui uma capacidade de gerenciar estados complexos de forma previsível, fazendo assim com que seja uma ferramento amplamente utilizada.
    * Também possui uma integração com o navegador a partir do Redux DevTools que possibilita o monitoramento dessas mudanças de estado, e possibilita que sejam feitas análises em relação à qualidade nos ambientes de produção.
    * E usaria o Toolkit pois ele facilita a configuração do Redux no código, pois reduz o boilerplate.
  * React Router para lidar com navegação
    * A flexibilidade para gerenciar rotas e maturidade dessa biblioteca que suporta tanto SPA's quanto multipáginas faz ela ser a escolha predominante em aplicações React
    * Permite fácil configuração de SSR e pre-rendering que são essencias para questões de SEO.
  * API Client usaria o AXIOS
    * Por possui interceptators ( que ajudam no geral a definir especificidades em requisições específicas ou no consumo http em geral ), timeout e cancelamento de requisições ela é majoritariamente usada para aplicações com essas stacks.
  * Ferramenta para Build seria o VITE
    * Possui configuração inicial mais simples e rápida. Possui tempo de build e hot reloading reduzidos também. Esse é um dos grandes motivos porque ela substituiu o create-react-app.
  * Para testes unitários eu escolheria JEST
    * É uma ferramenta extremamente robusta que tem possibilidade de oferecer testes de integração também, além da possibilidade de unitários.
- Dada a escolha das tecnolgias, a ideia para arquitetura seria voltada para microfrontends. Garantiria que a aplicação poderia escalar de forma independente, pois permite que diferentes equipes desenvolvam, implantem e escalem partes da aplicação de forma independente. Isso tudo gerenciado a partir de pacotes instalados no node_modules. A modularidade através da componentização que o React traz iria permitir que as partes da aplicação fossem reutilizadas ou substituídas facilmente. Procuraria também adotar alguma estratégia relacionada a código limpo, rotinas de revisão de código por membros da squad e techleads e procuraria formas de automatizar os testes para uma maior confiabilidade nas entregas.
- Caso fosse pensar em algo a mais para incrementar, seria usar um BFF para garantir desacomplamento. Como também fazer uso de Docker para garantir que seja escalável de forma horizontal e ter alguma implementação relacionada a monitoramento ou logging.
  
##

### Escalabilidade e Desempenho:

- A primeira ação que seria o entendimento do estado atual da aplicação e a identificação onde os problemas podem estar de fato acontecendo.
  * Essa análise de problemas poderiam ser feitas de forma primeiro a passar pelas principais jornadas da aplicação e fazer uma análise de tempo de render das telas e logo após analisar se essa demora estaria vindo de má estruturação de código, excesso de requisições ou seria algo relacionado ao serviços consumidos do back-end estarem demorando para fazer o retorno. A primeira parte iria consistir mais em monitoramente e coleta de informações sobre as jornadas.
  * Logo após descobrir quais são as jornadas com principais gargalos de desempenho, poderia ser realizado algum teste de carga e assim identificar dentro daquele fluxo qual o principal ponto de falha.
  * Para esta situação de monitoramento, poderíamos fazer uso do Google Analytics para monitorar o desempenho em tempo real e também pegar erro nas jornadas dos usuários.
- Poderia ser realizada também uma análise de tempo de carregamento de arquivos estáticos. Para cenários de análise de perfomance poderia ser utilizado o próprio DevTools e o Perfomance Panel para fazer análise de renderização.
- Analisar também as requisições de forma a ter a noção se está sendo realizado algum tipo de concorrência dada a múltiplas operações assíncronas ocorrendo ao mesmo tempo.
- Seria necessário também estabelecer uma rotina de melhoria contínua no front-end, com análises de perfomance, testes de usabilidade de acessibilidade para poder ter coleta de métricas de perfomance em tempo real e a partir disso traçar possíveis soluções.

##

### Manutenção e Evolução de Projeto:

- Para este caso em específico seria necessário dividir em etapas a solução, de forma a diminuir a dívida técnica a partir de uma atuação direcionada e ter um plano estruturado para tal.
  
  * 1ª Etapa: iria consistir em entender qual o estado atual da aplicação identificando áreas críticas onde teria dívida técnica e a partir disso planejar um processo de refactor. Poderia ser inicialmente feito a partir de revisão de código que possui duplicações, excesso de acomplamento e falta de testes unitários para esses locais. Uma parte extremamente importante seria ter o mapeamento das jornadas que são críticas para a atuação e disposição do negócio em si ( jornadas que impactam diretamente no lucro ) para ter uma atenção especial no processo de refactor. Após ter esse mapeamento das jornadas e locais que precisam de refactor, seria ideal criar um backlog estruturado e a partir disso definir metas para a refatoração.
  * 2º Etapa: tendo um backlog estruturado, poderíamos seguir para um cenário de análise de ambiente de teste para ver se o mesmo suporta grandes mudanças. Esse ambiente de testes teria que ser criado baseado no ambiente de produção, para ter testes mais assertividade no desenvolvimento e entregar ao cliente a melhora sem prejudicar sua jornada. Após isso, definir um gitflow para seguir de forma a estruturar a publicação e ter um versionamento tanto de código quanto da aplicação em si de forma mais assertiva. Em paralelo à um versionamento, seria importante estruturar um CI de forma a ter pipelines que testem automaticamente o código antes de subir para a branch ( isso em um cenário muito ideal ).
  * 3º Etapa: iniciar o refactor do código de forma incremental, separando por mini tarefas e realizando o fluxo de testes unitários para cada nova implementação e em paralelo melhorar a segurança e perfomance da aplicação, analisando aninhamento de loop, excesso de render. Ter rotinas de code review entre as squads é necessário e além disso fazer uso de ferramenta pra análise de código estático para o front ( ESLint ).
  * 4º Etapa: depois de fazer a verificação das etapas anteriores seria necessário garantir que a aplicação está pronta para ser publicada com segurança. Dado isto, seria necessário realizar testes regressivos ( de forma a passar pelas jornadas críticas e de mais impacto ao cliente ), realizar testes de seguranças ( pen tests ) para garantir que o refactor não trouxe novas vulnerabilidades e além de tudo realizar testes de perfomance para entender se está condizente com o esperado das jornadas ( tempo de loading, render e afins ).
  * 5º Etapa: após publicar o produto refatorado, seria necessário estabelecer uma cultura de monitoramento contínuo e melhoria contínua também para garantir que o produto continue viável para o uso.
  
##

### Integração com Back-end e APIs ( Coloquei no código a estrutura de pastas que eu criaria para esse fluxo ):

- Primeiro de tudo para ter um fluxo estrurado de integração, seria necessário criar a config de integração da API, instalação do axios e centralização de conexão com o serviço e implementação de interceptators nele. 
- Após realizar a config, seria necessário fazer a instalação de uma biblioteca de gerenciamento de estado global ( eu usaria o Redux com Redux Toolkit ), ao fazer essa centralização, faria com que toda a nossa aplicação tivesse conhecimento de qualquer requisição em qualquer parte do código, fazendo assim com que a aplicação possa conversar melhor entre si e até também reaproveitar requisições gerais criadas para outros fluxos mas que poderiam ser reutilizadas.
- Criar também dentro da pasta config um arquivo enviroment que controlaria nosso .env e a partir disso faria a identificação de ambiente e setaria as keys necessárias para cada ambiente
- Para as requisições que fossem reutilizadas, poderíamos fazer uma pasta de hooks, onde teríamos a personalização para cada caso.
- A estrutura seria então, diretório `src` que iria conter os diretórios `config (conexão com api), que teria o arquivo enviroment.ts`, `store ( local onde seria configurado o controle de estado global [REDUX]`, `hooks ( local onde teriam hooks personalizados em geral, não apenas os de requisição )`.
- A ideia geral é centralizar no redux todas as requisições e a partir disso criar uma arquitetura do código que consegue reutilizar tudo.

##

### Design e UX:

- A primeira etapa de criação de um design system está intrísecamente ligada à definições que têm que ser feitas como fundamentos que irão guiar o Design System. Primeiro teria que documentar todos os princípios como cores, tipografia, espaçamento, sombras e tamanhos. Isso seria em paralelo com o estabelicimento de boas práticas e acessibilidade também. Após essas definições, outro fluxo que seria necessário seria definir tokens de design para garantir consistência no que vai ser utilizado.
- A segunda seria a criação de componentes reutilizáveis. Seria criada uma biblioteca com componentes reutilizáveis e "coringas" de forma que possam ser modificados a partir de um componente base, como inputs, botões, modais e afins. A criação de um Storybook para documentar e demonstrar esses componentes seria algo extremamente poderoso.
- A criação dos componentes no código devem permitir temas, serem baseados em props ( para poder realizar mudanças no mesmo a partir da definição da propriedade ) e ter uma estruturação como um Atomic Design, de forma a separar os componentes em átomos, moléculas e organismos.
- O design system tem uma perspectiva de crescimento imensa quando é feita de forma a ser um repositório separado e integrado com um sistema de pacotes para poder publicar e versionar esse Design System. Num cenário ideal seria implementado um processo de CI/CD para publicar as alterações no design system de forma automaticamente testada.
- É importante também ter uma wiki que explique sobre os componentes, o que eles fazem, como implementar e como deve ser feito o uso de cada componente.

##

### Testes e Qualidade de Código:

- Para estruturar uma pipeline com CI/CD seria necessário configurar o ambiente de desenvolvimento do repositório para suportar continous integration. Para isso teríamos primeiro que seguir um gitflow para organizar o desenvolvimento e as releases, como também ter rotinas fixas de revisão de PR para ter garantia de qualidade de código.
- Tendo esse fluxo estruturado, viria o momento de configurar as etapas da pipeline, pois é necessário que o código seja testado em vários níveis antes de ser implantado.
  * Primeiro fluxo seria o linting e análise estática de código
  * Segundo fluxo seria testes unitários na pipe. Esses atuariam em funções, classes ou qualquer estrutura necessária no código.
  * Terceiro seria ter um fluxo de teste end-to-end para garantir que todas as partes da aplicação funcionem juntas
  * E o último passo seria o build e o deploy em si da aplicação. O github action poderia ser uma ferramenta para automatização de deploy.

##

### Adoção de Novas Tecnologias:

- Como a adoção de uma nova tecnologia pode ter impactos tanto positivos quanto negativos na produtividade, manutenção e em longo prazo na evolução da aplicação é algo a ser analisado com bastante calma e considerando muitos critérios. O primeiro caso de análise seria relacionado diretamente ao projeto atual. Entender em qual contexto se encontra o projeto e o que o novo framework que vai ser implementado deve atender.
- Seria necessário analisar cenários também como facilidade de integração, curva de aprendizado dos membros da squad para a nova ferramenta, produtividade que vai ser agredada ou retirada a partir da adesão do framework, manutenção a longo prazo da própria ferramenta, performance e a parte mais crucial para decidir essas novas implementações é o custo que vai ser gerado para a empresa.
- Uma ação que poderia ser tomada para isso seria realizar uma prova de conceito para testar o framework em um ambiente controlado, verificar se ele atende aos critérios que foram esperados e logo após isso fazer a análise dos resultados em relação aos critérios que foram usados para avaliar o framework.
- Entendo que a tomada de decisão só pode ser realizada após esses cenários serem concluídos.

## 

### Colaboração e Mentoria:

- Acho que em um primeiro momento seria fazer a análise do meu time e categorizar eles em relação à nível de conhecimento técnico. Este último sendo o primeiro ponto para levar em consideração para definir o nível de um integrante. Logo após tentaria montar times com uma separação onde teria um ponto focal ( este sendo o integrante mais experiente ) que seria responsável por ajudar os integrantes da sua equipe. Promover dinâmicas para identificar pontos fortes em cada integrante e estabelecer um canal direto de comunicação tanto comigo quanto com os outros líderes de outra equipe. Tornar um ambiente colaborativo. E promover interação entre as equipes de forma a cada equipe trazer como está a evolução e apresentar sobre algum assunto específico, para que o conhecimento seja fomentado por eles e para eles.
- Garantir que as tarefas fossem dividas de acordo com o nível de cada integrante
- Promover code reviews estruturados para garantir a qualidade de código e troca de conhecimento entre as equipes.
- Incentivar o uso de criação de documentação para jornadas, tecnologias e até novas tecnologias.
- E um dos pontos mais importantes, criar uma estrutura de feedback para todos os integrantes do time. De forma que possa contribuir para melhora individual de cada integrante e da equipe por conseguinte.


