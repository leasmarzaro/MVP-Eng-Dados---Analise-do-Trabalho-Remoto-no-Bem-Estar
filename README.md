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
4. Como a quantidade de e-mails enviados impacta na percepção de produtividade e no nível de estresse?
5. Como a quantidade de reuniões realizadas impacta na percepção de produtividade, de nível de estresse e equilíbrio entre trabalho e vida pessoal?
6. Como estar ativo fisicamente impacta os indicadores de produtividade, nível de estresse e equilírio entre trabalho e vida pessoal?   
7. Como a quantidade de tempo em frente à tela por dia impacta esses indicadores?  
8. Como a duração do sono impacta nesses indicadores? 
9. Como a quantidade de horas trabalhadas por dia impacta esses indicadores?  

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

<img width="399" alt="modelagem_raw" src="https://github.com/user-attachments/assets/84503472-7565-4f73-8695-4ebeb0ab9256" />

![tb_catalogo_arquivo_fonte](https://github.com/user-attachments/assets/9c0d46f5-4d48-40c7-a118-53336228ca81)

  
* **Camada Trusted**  
Dadas as análises anteriores de cada campo da tabela na camada raw, podemos inferir que os campos Employee_ID, Daily_Working_Hours, Screen_Time, Meetings_Attended, Emails_Sent, Physical_Activity_Steps, Sleep_Duration influenciam os indicadores Productivity_Score, Stress_Level e Work_Life_Balance_Satisfaction. Assim, foi escolhido o esquema estrela que será formado pelas dimensões dm_employee_id, dm_working_hour, dm_screen_time, dm_meeting_attended, dm_email_sent, dm_physical_activity_step, dm_sleep_duration e a fato fp_remote_work_wellbeing que contem os indicadores em questão.
<img width="880" alt="Captura de Tela 2025-04-11 às 16 44 22" src="https://github.com/user-attachments/assets/5b38c319-d717-4408-84f4-d8a92112e635" />

**dm_employee**
  
![catalogo_trusted_employee](https://github.com/user-attachments/assets/5456b58b-7774-4a01-b960-63cfc834a384)  

**dm_email_sent**  

![catalogo_trusted_email_sent](https://github.com/user-attachments/assets/3365b2aa-02f9-4b7a-b652-717440771827)  

**dm_meeting_attended**  

![catalogo_trusted_meeting_attended](https://github.com/user-attachments/assets/264e25e1-eb48-4fc6-a5f5-4b6222ca723c)

**dm_physical_activity**  

![catalogo_tusted_physical_activity](https://github.com/user-attachments/assets/712f483e-d440-46a1-ae49-949443511c2d)

**dm_screen_time**  

![catalogo_trusted_screen_time](https://github.com/user-attachments/assets/612aca83-1458-43fe-b68f-70bb5cb57117)  

**dm_sleep_duration**

![catalogo_trusted_sleep_duration](https://github.com/user-attachments/assets/6fdd9188-5035-4501-8bef-39416aff863f)  

**dm_working_hour**

![catalogo_trusted_working_hour](https://github.com/user-attachments/assets/0df539d2-b88d-4692-b6cf-18e5256983fc)

**fp_remote_work_wellbeing**

![catalogo_trusted_fp](https://github.com/user-attachments/assets/c24c8797-131c-4244-b300-abd75b8302f3)


* **Camada Refined**  
  Para realizar a análise dos indicadores com intuito de responder as perguntas formuladas, será criada uma tabela flat na camada refined para cada tabela de dimensão na camada refined.  
![modelagem_refined](https://github.com/user-attachments/assets/202f058a-c1ca-4ba7-bff9-b28fd8b49c32)

**tb_email_sent**

![catalogo_refined_email_enviado](https://github.com/user-attachments/assets/0ab61622-433e-4292-b7ce-2632522e6ac6)

**tb_physical_activity**

![catalogo_refined_atividade_fisica](https://github.com/user-attachments/assets/a46fa59e-b79b-494f-bcd6-2c71d586e3d9)

**tb_sleep_duration**

![catalogo_refined_duracao_sono](https://github.com/user-attachments/assets/60964866-beb5-404e-a3f6-ca4f4c64ca14)

**tb_working_hour**

![catalogo_refined_horas_trabalhadas](https://github.com/user-attachments/assets/47810ce4-2e33-4bf1-8761-05cebc888218)

**tb_meetings_attended**

![catalogo_refined_reunioes_realizadas](https://github.com/user-attachments/assets/551c62e4-a75d-4323-8168-3141b3560b7a)

**tb_screen_time**

![catalogo_refined_tempo_tela](https://github.com/user-attachments/assets/9202d264-fee4-4f9b-8784-004cd9586688)

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/gears.svg" width="25" height="25"> *Carga de Dados*
=

Todo o processo de carga de dados foi realizado através do databricks utilizando pyspark e pode ser visto em detalhes no notebook. 

* **Camada Raw**  
Vide notebook anexado.  
(https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/3610579466192528/3488375408189981/7772060516020031/latest.html)

* **Camada Trusted**  
Vide notebook anexado.  
(https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/3610579466192528/3488375408189981/7772060516020031/latest.html)

* **Camada Refined**  
Vide notebook anexado.  
(https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/3610579466192528/3488375408189981/7772060516020031/latest.html)


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/magnifying-glass-chart.svg" width="25" height="25"> *Análise de Dados*
=

<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/eye.svg" width="20" height="20"> *Qualidade de Dados*

* **Employee**  
Verificamos que a coluna Employee_ID possui valores únicos e não nulos. 
![qualidade_dados_employee](https://github.com/user-attachments/assets/591a8921-0f22-4b9f-994d-5cdec63ea0af)

Além disso, os dados estão anominizados respeitando a LGPD.

![qualidade_dados_employee_2](https://github.com/user-attachments/assets/82edcc6e-5f59-46e9-8fac-71031d64070c)


* **Working Hours**  
Podemos perceber que a coluna Daily_Working_Hours possui uma distruição uniforme entre 4 e 12h trabalhadas por dia.

![qualidade_dados_working_hours](https://github.com/user-attachments/assets/de9d1daf-7857-4c2a-a9c4-94f02639d01c)

![qualidade_dados_working_hours_2](https://github.com/user-attachments/assets/f19e12d3-3776-4be3-8ff5-b25769f17a5c)

Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.


* **Screen Time**  
Percebemos que a coluna Screen_Time possui uma distruição uniforme entre 3 e 10h.

![qualidade_dados_screen_time](https://github.com/user-attachments/assets/26e0a4d7-1b72-47d8-a649-9956d3942d1d)

![qualidade_dados_screen_time_2](https://github.com/user-attachments/assets/7c77f4a5-bd18-495c-89cf-2eef2cae4676)

Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* **Meetings_Attended**  
A coluna Meetings_Attended possui uma distruição uniforme entre 0 e 7.

![qualidade_dados_screen_time](https://github.com/user-attachments/assets/be5b4ccf-7b8f-44cf-8231-8fa5e92e897b)

![qualidade_dados_screen_time_2](https://github.com/user-attachments/assets/5ae509c0-c4d5-4d26-895d-861be8627fd3)


* **Emails_Sent**  
Percebemos que a coluna Emails_Sent possui uma distruição uniforme entre 5 e 99.

![qualidade_dados_emails_sent](https://github.com/user-attachments/assets/df8e6468-166c-4c61-9525-51ce62f2688e)

![qualidade_dados_emails_sent_2](https://github.com/user-attachments/assets/b9640f59-d63c-4793-a655-7bf107766803)

Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* **Productivity_Score**  
Verificamos que o indicador Productivity_Score não possui valores nulos e que eles variam entre 1 a 10.

![qualidade_dados_productivity_score](https://github.com/user-attachments/assets/fa6cb8e4-a1dd-41b4-8646-06699c9e3de7)

![qualidade_dados_productivity_score_2](https://github.com/user-attachments/assets/45091628-ce57-45ab-8ddd-cc47bf84302d)

* **Stress_Level**  
Verificamos que o indicador Stress_Level não possui valores nulos e que eles variam entre 1 a 10.

![qualidade_dados_stress_level](https://github.com/user-attachments/assets/3cf1fb36-c87c-47a4-88fd-8a003564ec5d)

![qualidade_dados_stress_level_2](https://github.com/user-attachments/assets/2e040d45-d2cf-42ec-9803-94b3dcae04d4)

* **Physical_Activity_Steps**  
Esta coluna possui mais de 7 mil registros em um intervalo de distruição entre 1000 e 14000.

![qualidade_physical_activity](https://github.com/user-attachments/assets/51e349f1-91bf-4771-aceb-417809fb9989)

![qualidade_physical_activity_2](https://github.com/user-attachments/assets/380cc322-ede8-4a36-8c6c-2c755b44d830)

Dessa forma, será feita a discretização dos valores encontrados para facilitar as análises futuras.

* **Sleep_Duration**  
Percebemos que a coluna Sleep_Duration possui uma distruição uniforme entre 4 e 9 horas.

![qualidade_dados_sleep_duration](https://github.com/user-attachments/assets/339a3608-8b4e-4e89-b0d3-3378343f58f9)

![qualidade_dados_sleep_duration_2](https://github.com/user-attachments/assets/b96e5083-436c-4e45-ba63-ab46a45579ed)

Para realizar a carga na próxima camada e facilitar as análises finais será feita a discretização dos valores encontrados.

* **Work_Life_Balance_Satisfaction**  
Verificamos que o indicador Work_Life_Balance_Satisfaction não possui valores nulos. E, que eles variam entre 1 a 10.

![qualidade_dados_work_life](https://github.com/user-attachments/assets/27b45d54-7e7f-41ed-8574-0d2324845931)

![qualidade_dados_work_life_2](https://github.com/user-attachments/assets/1e5331d8-ab22-4326-9825-57178a13c809)


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/brain.svg" width="20" height="20"> *Solução do Problema*

Para o grupo de 10.000 empregados em trabalho remoto, temos:  
1. **Qual o nível médio da produtividade percebida por esses trabalhadores?**  
    A média de produtividade percebida é 5.54.

2. **Qual o nível médio do estresse percebido por esses trabalhadores?**  
    A média de nível de estresse é 5.53.  

3. **Qual o nível médio do equilíbrio entre vida profissional e pessoal percebido por esses trabalhadores?**  
    A média de equilíbrio é 5.48.  

Essas médias serão utilizadas como base de comparação para as demais análises. 

4. **Como a quantidade de e-mails enviados impactam na percepção de produtividade, nível de estresse e equilíbrio entre trabalho e vida pessoal?**

![analise_email_enviado](https://github.com/user-attachments/assets/de0e9fe4-ac97-40d3-b6d1-3b655b4cac8d)

**_Produtividade:_**
O indicador cresce até apresentar o valor máximo na faixa de 30 a 40 e-mails enviados. Após isso, ele decresce ficando sempre abaixo da média geral. Para os trabalhadores remotos, podemos inferir que entre 30 a 40 e-mails por dia são suficientes para atingir uma produtividade ótima. 

**_Nível de estresse:_**
O nível de estresse alcança seu valor máximo na faixa de 20 a 30 e-mails enviados e após essa faixa segue uma tendência de valor abaixo da média geral. Assim sendo, percebemos que ao atingir o nível de estresse máximo o aumento no volume de e-mails não gera aumento no indicador.

**_Equilíbrio entre trabalho e vida pessoal:_** 
Este indicador possuiu o comportamento similar ao indicador de produtividade, tendo o seu ponto ótimo na faixa de 30 a 40 e-mails enviados. Este dado parece ser coerente uma vez que, intuitivamente, associamos uma boa produtividade ao equilíbrio entre vida profissinal e pessoal.

5. **Como a quantidade de reuniões realizadas por dia impacta na percepção de produtividade e de nível de estresse?**

![analise_reuniao_feitas](https://github.com/user-attachments/assets/aa5f9928-b507-4108-a17c-f44f4cafefe0)

**_Produtividade:_**
A percepção de produtividade é maior para os empregados que realizam até 2 reuniões decaindo ao valor mínimo da série para a faixa de 3 a 5 reuniões. Entretanto, o aumento do indicador na faixa 'Mais de 6 reuniões' pode estar associado a facilidade que o trabalho remoto traz para troca de contexto e a realização de multiplas reuniões em um intevalo curto de tempo.

**_Nível de estresse:_**
Conforme esperado, o aumento no número de reuniões realizadas implica o aumento na percepção do nível de estresse dos trabalhadores remotos.

**_Equilíbrio entre trabalho e vida pessoal:_**
Percebemos que esse indicador tem comportamento similar ao indicador de nível de estresse, onde o aumento no número de reuniões realizadas durante o dia implica o aumento do indicador de equilibrio. Este fato pode ser explicado pela facilidade do empregado em poder conciliar atividades pessoais ou otimizar o seu tempo o que seria mais complexo com o trabalho presencial.

6. **Como estar ativo fisicamente impacta os indicadores de produtividade, nível de estresse e equilírio entre trabalho e vida pessoal?**

![analise_atividade_fisica](https://github.com/user-attachments/assets/da503749-e07a-45a1-a017-3b0df08aad6a)

**_Produtividade:_**
De uma forma geral, o aumento no número de passos parece contribuir para a aumento do indicador de produtividade percebida chegando a um valor ótimo na faixa de 9000 a 10000 passos. Os outliers nas faixas 6000 a 9000 passos e '12000 a 13000 passos' deveriam ser estudadas, pois ficam abaixo da média global.

**_Nível de estresse:_**
Conforme esperado, o aumento no número de passos reflete uma redução do nível de estresse percebido. O indicador aumenta a partir de 12000 passos o que pode estar relacionado a um excesso de atividade ou fadiga.

**_Equilíbrio entre trabalho e vida pessoal:_**
Assim como no indicador de produtividade, o aumento do número de passos parece impactar diretamente na melhora da percepção do equilíbrio entre trabalho e vida pessoal.

7. **Como a quantidade de tempo em frente à tela por dia impacta esses indicadores?**

![analise_tempo_tela](https://github.com/user-attachments/assets/6db8aaba-88db-4b0b-b665-c4244a5bd2e2)

**_Produtividade:_**
Não foi possível identificar um padrão de comportamento, pois a faixa '5h a 7h usando tela' possui muito inferior em relação as demais.

**_Nível de estresse:_**
Apesar do nível de estresse ser mais alto no faixa de maior tempo de tela, não foi possível identificar um padrão uma vez que no intervalo de 5h a 9h os valores são bem inferiores ao valor da faixa inicial e à média geral.

**_Equilíbrio entre trabalho e vida pessoal:_**
O mesmo ocorre nesse indicador, embora atinja o valor mínimo na faixa de maior tempo de tela não foi possível identificar um padrão considerando as demais faixas.

8. **Como o tempo de duração do sono impacta nesses indicadores?**

![analise_duracao_sono](https://github.com/user-attachments/assets/e281e2f0-aabf-4b9d-88fc-313a4aeed61c)

**_Produtividade:_**
Conforme esperado, o aumento na quantidade de horas de sono tem uma relação positiva com o indicador de produtividade percebida tendo seu ponto máximo na faixa de 7 a 8 horas de sono. O fato da percepção de produtividade diminuir na faixa de mais de 8h de sono precisaria de uma análise mais elaborada podendo estar associada a outros indicadores de bem estar.
 
**_Nível de estresse:_**
De forma contraituitiva, o nível de estresse percebido aumenta conforme aumenta a quantidade de horas de sono. Esta relação precisaria ser estudada e entendida em mais detalhes para melhor avaliação deste resultado.

**_Equilíbrio entre trabalho e vida pessoal:_**
Podemos verificar que esse indicador possui o valor máximo na faixa de '8h a 9' de duração de sono. Este indicador parece estar coerente uma vez que o trabalho remoto tende a permitir que os trabalhadores aproveitem melhor a ausência do tempo de deslocamento para outras atividades, incluindo o sono.

9. **Como a quantidade quantidade de horas trabalhadas por dia impacta esses indicadores?**

![analise_horas_trabalhadas](https://github.com/user-attachments/assets/025bb471-ce3e-421c-b1b0-7161f82f5430)

**_Produtividade:_**
De acordo com o esperado, podemos observar que a produtividade percebida possui seu valor máximo no intervalo 6h a 8h trabalhadas e esta  diminiu com o aumento da quantidade de horas trabalhadas. Esta distribuição parece ser coerente uma vez que mais horas de trabalho podem estar associadas a uma baixa produtividade ou dificuldades percebidas para a realização de atividades em modelo remoto.

**_Nível de estresse:_**
Analogamente, o nível de estresse possui seu valor mínimo no intervalo 6h a 8h trabalhadas e ele aumenta com o aumento da quantidade de horas trabalhadas.

**_Equilíbrio entre trabalho e vida pessoal:_**
Percebemos que esse indicador possui um comportamento linear, ou seja, ele aumenta com o aumento da quantidade de horas trabalhadas. Esse resultado vai de encontro com o esperado, e, provavelmente, este fato possa ser explicado pela facilidade do empregado em poder conciliar atividades pessoais ou otimizar o seu tempo o que seria mais complexo com o trabalho presencial.


<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/user-graduate.svg" width="25" height="25"> *Autoavaliação*
=

De uma forma geral, foi possível responder todas as perguntas formuladas e que eram alvo do objetivo deste trabalho. Entretanto, algumas das análises não foram conclusivas dando margem para a expansão e aprofundamento do trabalho através de análises mais robustas, como por exemplo, a correlação de multiplas variáveis com os indicadores base da análise. Também vejo, como uma possibilidade de extensão deste trabalho buscar correlação com outros datasets que explorem uma industria específica, como a industria de TI no Brasil.

Para este primeiro MVP não tive dificuldade em definir um tema para o trabalho, todavia encontrar um dataset de qualidade sobre o trabalho remoto se mostrou mais complexo do que o previsto. Outro ponto relevante é que acabei por utilizar todo o prazo para execução do trabalho, pois o volume de conteúdo e tecnologias a serem estudadas e apreendidas se demostrou elevado.

Sendo assim, posso afirmar que fiquei satisfeita com o resultado final do trabalho, pois considero que consegui aplicar todos os conceitos e ferramentas vistos ao longo do curso.


