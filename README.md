# MVP Engenharia de Dados 
Análise do impacto do trabalho remoto na produtividade, saúde mental e equilíbrio entre trabalho e vida pessoal.

Trabalho desenvolvido para o Curso de Pós-Graduação em Ciência de Dados e Analytics da PUC-RJ.

Aluna: _Léa Juliane Smarzaro das Chagas Caseira_

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/bullseye.svg" width="25" height="25"> *Objetivo*
=
Existe uma discussão corrente sobre políticas de retorno ao escritório após o fim da pandemia de COVID-19. Essa discussão gira em torno da necessidade das empresas em aumentar a produtividade e o engajamento dos seus funcionários. Entretanto, são poucas as análises feitas sobre a percepção dos profissionais que trabalham remotamente com relação à produtividade, ao estresse e ao equilíbrio entre vida profissional e pessoal.  
Nesse sentido, foi escolhido um conjunto de dados com estes indicadores para responder as seguintes perguntas:  
1. Qual o nível médio da produtividade percebida por esses trabalhadores?  
2. Qual o nível médio do nível de estresse percebido por esses trabalhadores?  
3. Qual o nível médio do equilíbrio entre trabalho e vida pessoal percebido por esses trabalhadores?  
4. Como a quantidade de horas trabalhadas por dia impacta esses indicadores?  
5. Como a quantidade de tempo em frente à tela por dia impacta esses indicadores?  
6. Como a quantidade de reuniões realizadas impacta na percepção de produtividade, de nível de estresse e equilíbrio entre trabalho e vida pessoal?  
7. Como a quantidade de e-mails enviados impacta na percepção de produtividade e no nível de estresse?  
8. Como a duração do sono impacta nesses indicadores?  
9. Como estar ativo fisicamente impacta os indicadores de produtividade, nível de estresse e equilírio entre trabalho e vida pessoal?  

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/database.svg" width="25" height="25"> *Coleta de Dados*
=
Para realizar essas análises, utilizamos a base de dados:  
  * Nome do conjunto de dados: Global Remote Work & Wellbeing Dataset  
  * Descrição: Análise da produtividade, saúde mental e equilíbrio entre vida profissional e pessoal no trabalho remoto.  
  * Formato dos dados: CSV  
  * Fonte dos dados: A estrutura conceitual para o conjunto de dados foi influenciada por informações coletadas de ferramentas de produtividade (monitorando horas de trabalho diárias, tempo de tela e volume de e-mail), dispositivos de saúde vestíveis (capturando atividade física, como contagem de passos e duração do sono) e pesquisas com funcionários (relatando métricas subjetivas, como produtividade, estresse e satisfação com o equilíbrio entre vida pessoal e profissional). Pesquisas publicadas e relatórios do setor sobre trabalho remoto, incluindo estudos disponíveis em plataformas como Kaggle e artigos de veículos de notícias respeitáveis, informaram os intervalos e distribuições realistas usados no conjunto de dados.  
  * Acesso: Os dados são públicos, gratuitos, estão normalizados e anonimizados.  
  * Link: https://www.kaggle.com/datasets/adilshamim8/global-remote-work-and-wellbeing-dataset/data  
  * Qualidade dos dados: Alta  
  * Responsável: Adil Shamim  
  * Data da última atualização: Fevereiro de 2025
     
Esses dados foram coletados e armazenados na plataforma Databricks Community onde também foi feito o desenvolvimento para a realização das análises.  

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/cubes.svg" width="25" height="25"> *Modelagem*
=
* **Camada Raw**
  
* **Camada Trusted**

Dadas as análises anteriores de cada campo da tabela na raw, podemos inferir que os campos Employee_ID, Daily_Working_Hours, Screen_Time, Meetings_Attended, Emails_Sent, Physical_Activity_Steps, Sleep_Duration influenciam os indicadores Productivity_Score, Stress_Level e Work_Life_Balance_Satisfaction. Assim, foi escolhido o esquema estrela que será formado pelas dimensões dm_employee_id, dm_working_hour, dm_screen_time, dm_meeting_attended, dm_email_sent, dm_physical_activity_step, dm_sleep_duration e a fato fp_remote_work_wellbeing que contem os indicadores em questão.
<img width="880" alt="Captura de Tela 2025-04-11 às 16 44 22" src="https://github.com/user-attachments/assets/5b38c319-d717-4408-84f4-d8a92112e635" />

* **Camada Refined**

Para realizar a análise dos indicadores com intuito de responder as perguntas formuladas será criada uma tabela flat na camada refined para cada tabela de dimensão na camada refined.  


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/gears.svg" width="25" height="25"> *Carga de Dados*
=
* **Camada Raw**
Vide notebook anexado.

* **Camada Trusted**
Vide notebook anexado.

* **Camada Refined**
Vide notebook anexado.

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/magnifying-glass-chart.svg" width="25" height="25"> *Análise de Dados*
=

Para o grupo de 10.000 empregados em trabalho remoto, temos:  
1. Qual o nível médio da produtividade percebida por esses trabalhadores?  
    A média de produtividade percebida é 5.54.  
2. Qual o nível médio do estresse percebido por esses trabalhadores?  
    A média de nível de estresse é 5.53.  
3. Qual o nível médio do equilíbrio entre vida profissional e pessoal percebido por esses trabalhadores?  
    A média de equilíbrio é 5.48.  

Essas médias serão utilizadas como base de comparação para as demais análises.  


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/eye.svg" width="20" height="20"> *Qualidade de Dados*

* Employee  
Verificamos que a coluna Employee_ID possui valores únicos e não nulos. Além disso, os dados estão anominizados respeitando a LGPD.

* Working Hours  
Podemos perceber que a coluna Daily_Working_Hours possui uma distruição uniforme entre 4 e 12h trabalhadas por dia. Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* Screen Time  
Percebemos que a coluna Screen_Time possui uma distruição uniforme entre 3 e 10h. Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* Meetings_Attended
A coluna Meetings_Attended possui uma distruição uniforme entre 0 e 7.

* Emails_Sent
Percebemos que a coluna Emails_Sent possui uma distruição uniforme entre 5 e 99. Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* Productivity_Score
Verificamos que o indicador Productivity_Score não possui valores nulos e que eles variam entre 1 a 10.

* Stress_Level
Verificamos que o indicador Stress_Level não possui valores nulos e que eles variam entre 1 a 10.

* Physical_Activity_Steps
Esta coluna possui mais de 7 mil registros em um intervalo de distruição entre 1000 e 14000. Dessa forma, será feita a discretização dos valores encontrados para facilitar as análises futuras.

* Sleep_Duration
Percebemos que a coluna Sleep_Duration possui uma distruição uniforme entre 4 e 9 horas. Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* Work_Life_Balance_Satisfaction
Verificamos que o indicador Work_Life_Balance_Satisfaction não possui valores nulos. E, que eles variam entre 1 a 10.


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/brain.svg" width="20" height="20"> *Solução do Problema*

* Como a quantidade de e-mails enviados impactam na percepção de produtividade, nível de estresse e equilíbrio entre trabalho e vida pessoal?

**_Produtividade:_**
O indicador cresce até apresentar o valor máximo na faixa de 30 a 40 e-mails enviados. Após isso, ele decresce ficando sempre abaixo da média geral. Para os trabalhadores remotos, podemos inferir que entre 30 a 40 e-mails por dia são suficientes para atingir uma produtividade ótima. 

**_Nível de estresse:_**
O nível de estresse alcança seu valor máximo na faixa de 20 a 30 e-mails enviados e após essa faixa segue uma tendência de valor abaixo da média geral. Assim sendo, percebemos que ao atingir o nível de estresse máximo o aumento no volume de e-mails não gera aumento no indicador.

**_Equilíbrio entre trabalho e vida pessoal:_** 
Este indicador possuiu o comportamento similar ao indicador de produtividade, tendo o seu ponto ótimo na faixa de 30 a 40 e-mails enviados. Este dado parece ser coerente uma vez que, intuitivamente, associamos uma boa produtividade ao equilíbrio entre vida profissinal e pessoal.

* Como a quantidade de reuniões realizadas por dia impacta na percepção de produtividade e de nível de estresse?

**_Produtividade:_**
A percepção de produtividade é maior para os empregados que realizam até 2 reuniões decaindo ao valor mínimo da série para a faixa de 3 a 5 reuniões. Entretanto, o aumento do indicador na faixa 'Mais de 6 reuniões' pode estar associado a facilidade que o trabalho remoto traz para troca de contexto e a realização de multiplas reuniões em um intevalo curto de tempo.

**_Nível de estresse:_**
Conforme esperado, o aumento no número de reuniões realizadas implica o aumento na percepção do nível de estresse dos trabalhadores remotos.

**_Equilíbrio entre trabalho e vida pessoal:_**
Percebemos que esse indicador tem comportamento similar ao indicador de nível de estresse, onde o aumento no número de reuniões realizadas durante o dia implica o aumento do indicador de equilibrio. Este fato pode ser explicado pela facilidade do empregado em poder conciliar atividades pessoais ou otimizar o seu tempo o que seria mais complexo com o trabalho presencial.

* Como estar ativo fisicamente impacta os indicadores de produtividade, nível de estresse e equilírio entre trabalho e vida pessoal?

**_Produtividade:_**
De uma forma geral, o aumento no número de passos parece contribuir para a aumento do indicador de produtividade percebida chegando a um valor ótimo na faixa de 9000 a 10000 passos. Os outliers nas faixas 6000 a 9000 passos e '12000 a 13000 passos' deveriam ser estudadas, pois ficam abaixo da média global.

**_Nível de estresse:_**
Conforme esperado, o aumento no número de passos reflete uma redução do nível de estresse percebido. O indicador aumenta a partir de 12000 passos o que pode estar relacionado a um excesso de atividade ou fadiga.

**_Equilíbrio entre trabalho e vida pessoal:_**
Assim como no indicador de produtividade, o aumento do número de passos parece impactar diretamente na melhora da percepção do equilíbrio entre trabalho e vida pessoal.

* Como a quantidade de tempo em frente à tela por dia impacta esses indicadores?

**_Produtividade:_**
Não foi possível identificar um padrão de comportamento, pois a faixa '5h a 7h usando tela' possui muito inferior em relação as demais.

**_Nível de estresse:_**
Apesar do nível de estresse ser mais alto no faixa de maior tempo de tela, não foi possível identificar um padrão uma vez que no intervalo de 5h a 9h os valores são bem inferiores ao valor da faixa inicial e à média geral.

**_Equilíbrio entre trabalho e vida pessoal:_**
O mesmo ocorre nesse indicador, embora atinja o valor mínimo na faixa de maior tempo de tela não foi possível identificar um padrão considerando as demais faixas.

* Como o tempo de duração do sono impacta nesses indicadores?

**_Produtividade:_**
Conforme esperado o aumento na quantidade de horas de sono tem uma relação positiva com o indicador de produtividade percebida tendo seu ponto máximo na faixa de 7 a 8 horas de sono. O fato da percepção de produtividade diminuir na faixa de mais de 8h de sono precisaria de uma análise mais elaborada podendo estar associada a outros indicadores de bem estar..
 
**_Nível de estresse:_**
De forma contraituitiva o nível de estresse percebido aumenta conforme aumenta a quantidade de horas de sono. Esta relação precisaria ser estudada e entendida em mais detalhes para melhor avaliação deste resultado.

**_Equilíbrio entre trabalho e vida pessoal:_**
Podemos verificar que esse indicador possui o valor máximo na faixa de '8h a 9' de duração de sono. Este indicador parece estar coerente uma vez que o trabalho remoto tende a permitir que os trabalhadores aproveitem melhor a ausência do tempo de deslocamento para outras atividades, incluindo o sono.

* Como a quantidade quantidade de horas trabalhadas por dia impacta esses indicadores?

**_Produtividade:_**
De acordo com o esperado, podemos observar que a produtividade percebida possui seu valor máximo no intervalo 6h a 8h trabalhadas e esta  diminiu com o aumento da quantidade de horas trabalhadas. Esta distribuição parece ser coerente uma vez que mais horas de trabalho podem estar associadas a uma baixa produtividade ou dificuldades percebidas para a realização de atividades em modelo remoto.

**_Nível de estresse:_**
Analogamente, o nível de estresse possui seu valor mínimo no intervalo 6h a 8h trabalhadas e ele aumenta com o aumento da quantidade de horas trabalhadas.

**_Equilíbrio entre trabalho e vida pessoal:_**
Percebemos que esse indicador possui um comportamento linear, ou seja, ele aumenta com o aumento da quantidade de horas trabalhadas. Esse resultado vai de encontro com o esperado, e, provavelmente, este fato possa ser explicado pela facilidade do empregado em poder conciliar atividades pessoais ou otimizar o seu tempo o que seria mais complexo com o trabalho presencial.




<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/user-graduate.svg" width="25" height="25"> *Autoavaliação*
=

