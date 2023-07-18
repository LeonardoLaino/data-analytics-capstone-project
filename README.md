# Desenvolvimento de uma Pipeline Completa para Chatbot no Telegram Utilizando a AWS

--------
### Contexto

Os chatbots têm ganhado cada vez mais popularidade como uma forma eficiente de comunicação entre empresas e clientes. Esses assistentes virtuais são capazes de responder perguntas, fornecer informações e até mesmo realizar transações, tudo de forma automatizada e interativa.

No contexto de chatbots, a coleta e análise de dados desempenham um papel fundamental. A informação gerada a partir das interações dos usuários com o chatbot pode ser extremamente valiosa para a empresa. Esses dados, no entanto, podem ser divididos em duas categorias distintas: `dados transacionais` e `dados analíticos`.

Os `dados transacionais` referem-se a informações específicas de cada interação do usuário com o chatbot. Isso inclui mensagens enviadas, comandos executados e transações realizadas. Esses dados são cruciais para garantir que o chatbot funcione corretamente e forneça respostas precisas e relevantes aos usuários em tempo real.

Já os `dados analíticos` são dados agregados e processados a partir das interações do usuário ao longo do tempo. Eles ajudam a compreender padrões de comportamento dos usuários, identificar tendências, realizar análises preditivas e extrair insights que podem direcionar decisões estratégicas da empresa.


### Resumo
O projeto consiste na criação de uma pipeline completa de dados utilizando a AWS para um chatbot no aplicativo Telegram, que permite aos usuários interagirem enviando mensagens para o bot. Essas mensagens são captadas em tempo real através da API de bots do Telegram e redirecionadas por meio de um Webhook do `AWS API Gateway`.

As mensagens redirecionadas passam por uma etapa de processamento simplificada, usando uma função do `AWS Lambda`. Os dados resultantes são armazenados no formato ".json" na primeira camada de um Data Lake (`AWS S3`), onde são organizados e particionados por data.

Diariamente, em um horário fixo pré determinado, um processo automatizado é acionado pelo `AWS Event Bridge`. Esse processo consiste em um ETL (Extração, Transformação e Carga), extraindo todos os dados "crus" do dia anterior na primeira camada do Data Lake. Os dados são então processados e enriquecidos por meio de outra função do `AWS Lambda` e são armazenados na segunda camada do Data Lake. Nessa segunda camada, os dados são armazenados no formato `.parquet`, ainda particionados por data, porém estruturados em tabelas através do `PyArrow`.

Foi então criada uma tabela no `AWS Athena`, permitindo acesso rápido e simplificado dos dados já processados, prontos para serem analisados e transformados em insights.

### Objetivo
O objetivo do projeto foi implementar uma pipeline completa e eficiente de dados utilizando a AWS, em um chatbot do Telegram, possibilitando a captura, armazenamento e processamento dos dados enviados pelos usuários. Com a infraestrutura montada, os dados foram preparados para análises posteriores, permitindo a extração de informações úteis e insights relevantes para a tomada de decisões.

### Benefícios
1. **Automação:** O processo de captura e processamento dos dados é totalmente automatizado, permitindo atualizações diárias sem intervenção manual.

2. **Economia de Recursos:** A infraestrutura baseada na AWS permite dimensionar recursos de acordo com a demanda, otimizando custos. Adicionalmente, a utilização de dados particionados e salvos em formatos adequados (como Apache Parquet), permite a realização de queries mais eficientes, economizando recursos computacionais e, por consequencia, utilizando menos recursos financeiros.

3. **Flexibilidade:** A utilização do Data Lake e o armazenamento em formatos distintos (".json" e ".parquet") proporcionam flexibilidade no tratamento e análise dos dados, inclusive permitindo reprocessamento.

4. **Rastreabilidade:** A estrutura de particionamento por data no Data Lake facilita a rastreabilidade dos dados, permitindo análises históricas precisas.

### Resultados
O pipeline de dados foi implementada com sucesso, capaz de captar mensagens enviadas pelos usuários no chat do Telegram e processá-las automaticamente em tempo real, armazenando-as de forma organizada utilizando particionamento dos dados brutos e enriquecidos. Os analistas podem extrair insights valiosos por meio dos dados coletados utilizando o AWS Athena, possibilitando uma análise detalhada e auxiliando em decisões estratégicas.