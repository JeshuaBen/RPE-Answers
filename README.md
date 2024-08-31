# RPE-Answers

### Arquitetura de Front-end:

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

### Manutenção e Evolução de Projeto

- Para este caso em específico seria necessário dividir em etapas a solução, de forma a diminuir a dívida técnica a partir de uma atuação direcionada e ter um plano estruturado para tal.
  
  * 1ª Etapa: iria consistir em entender qual o estado atual da aplicação identificando áreas críticas onde teria dívida técnica e a partir disso planejar um processo de refactor. Poderia ser inicialmente feito a partir de revisão de código que possui duplicações, excesso de acomplamento e falta de testes unitários para esses locais. Uma parte extremamente importante seria ter o mapeamento das jornadas que são críticas para a atuação e disposição do negócio em si ( jornadas que impactam diretamente no lucro ) para ter uma atenção especial no processo de refactor. Após ter esse mapeamento das jornadas e locais que precisam de refactor, seria ideal criar um backlog estruturado e a partir disso definir metas para a refatoração.
  * 2º Etapa: tendo um backlog estruturado, poderíamos seguir para um cenário de análise de ambiente de teste para ver se o mesmo suporta grandes mudanças. Esse ambiente de testes teria que ser criado baseado no ambiente de produção, para ter testes mais assertividade no desenvolvimento e entregar ao cliente a melhora sem prejudicar sua jornada. Após isso, definir um gitflow para seguir de forma a estruturar a publicação e ter um versionamento tanto de código quanto da aplicação em si de forma mais assertiva. Em paralelo à um versionamento, seria importante estruturar um CI de forma a ter pipelines que testem automaticamente o código antes de subir para a branch ( isso em um cenário muito ideal ).
  * 3º Etapa: iniciar o refactor do código de forma incremental, separando por mini tarefas e realizando o fluxo de testes unitários para cada nova implementação e em paralelo melhorar a segurança e perfomance da aplicação, analisando aninhamento de loop, excesso de render. Ter rotinas de code review entre as squads é necessário e além disso fazer uso de ferramenta pra análise de código estático para o front ( ESLint ).
  * 4º Etapa: depois de fazer a verificação das etapas anteriores seria necessário garantir que a aplicação está pronta para ser publicada com segurança. Dado isto, seria necessário realizar testes regressivos ( de forma a passar pelas jornadas críticas e de mais impacto ao cliente ), realizar testes de seguranças ( pen tests ) para garantir que o refactor não trouxe novas vulnerabilidades e além de tudo realizar testes de perfomance para entender se está condizente com o esperado das jornadas ( tempo de loading, render e afins ).
  * 5º Etapa: após publicar o produto refatorado, seria necessário estabelecer uma cultura de monitoramento contínuo e melhoria contínua também para garantir que o produto continue viável para o uso.
  
##

### Integração com Back-end e APIs ( Coloquei no código a estrutura de pastas que eu criaria para esse fluxo )

- Primeiro de tudo para ter um fluxo estrurado de integração, seria necessário criar a config de integração da API, instalação do axios e centralização de conexão com o serviço e implementação de interceptators nele. 
 * Após realizar a config, seria necessário fazer a instalação de uma biblioteca de gerenciamento de estado global ( eu usaria o Redux com Redux Toolkit ), ao fazer essa centralização, faria com que toda a nossa aplicação tivesse conhecimento de qualquer requisição em qualquer parte do código, fazendo assim com que a aplicação possa conversar melhor entre si e até também reaproveitar requisições gerais criadas para outros fluxos mas que poderiam ser reutilizadas.
 * Criar também dentro da pasta config um arquivo enviroment que controlaria nosso .env e a partir disso faria a identificação de ambiente e setaria as keys necessárias para cada ambiente
 * Para as requisições que fossem reutilizadas, poderíamos fazer uma pasta de hooks, onde teríamos a personalização para cada caso.
 * A estrutura seria então, diretório `src` que iria conter os diretórios `config (conexão com api), que teria o arquivo enviroment.ts`, `store ( local onde seria configurado o controle de estado global [REDUX]`, `hooks ( local onde teriam hooks personalizados em geral, não apenas os de requisição )`.
 * A ideia geral é centralizar no redux todas as requisições e a partir disso criar uma arquitetura do código que consegue reutilizar tudo.

##

### Design e UX




