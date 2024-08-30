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

- 
