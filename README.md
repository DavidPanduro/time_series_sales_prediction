# Predição de Séries Temporais de Vendas
Por David Panduro :computer:<br><br>
![image](https://github.com/DavidPanduro/time_series_sales_prediction/assets/45201867/44c25336-5bde-4127-baca-a3f4f924b62f)<br><br>


Analisaremos os **dados de vendas** de uma das lojas de uma grande **rede de supermercados**, a fim de fazer predições das vendas dos **próximos 30 dias**. <br>
A base geral conta com pouco mais de 01 milhão de registros. Mas inclui todas as lojas da rede de supermercados. Neste caso, por motivos de praticidade, filtraremos uma (01) loja para aplicar os conceitos de séries temporais nele. A base de amostra final fica com 942 registros, com as seguintes colunas:<br><br>

  01. Date ==> É a data do evento. Está na granuladidade diária. É de tipo object, mas terá que ser convertido a índice.<br>
  02. Sales==> É a quantidade monetária total das vendas diárias. É de tipo int, mas será convertido a float.<br><br>

![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/736b52ec-0b0c-48ec-bdcd-3363ad6a43da)<br>
<p style="text-align: center;">Fig.01. Dataset Sales </p><br><br>
     
Aplicaremos métodos da estatística e de aprendizado de máquina: Visando aplicar Auto-Arima, Arima, Arma. Assim como, MultiLayer Perceptron.<br><br>

**Os resultados** obtidos em cada parte do processo, seguen a continuação: <br><br>

  01. Visualização da série.<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/803a620e-656e-47e7-84f2-e8652a8f8747)<br>
  <p style="text-align: center;">Fig.02. Dataset Sales - Filter Store 01</p><br><br>

  02. Decomposição da série.<br><br>  

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/025fb3a8-8609-4fe9-8b72-8522afbf20ce) <br>
  <p style="text-align: center;">Fig.03. Seasonal Decomposition of Sales Dataset</p><br><br>
  03. Visualização da Autocorrelação da série.<br><br>
  
  ![image](https://github.com/DavidPanduro/time_series_prediction/blob/master/img/acp_sales.jpg)<br>
  <p style="text-align: center;">Fig.04. Autocorrelation of Sales Dataset</p><br>
  04. Visualização da Autocorrelação Parcial da série.<br><br>  
  
  ![image](https://github.com/DavidPanduro/time_series_prediction/blob/master/img/pacf_sales.jpg).<br>
  <p style="text-align: center;">Fig.05. Autocorrelation Partial of Sales Dataset </p><br>
  05. Testes de Estacionaridade. Augmented Dickey-Fuller (ADF).<br><br>
  
  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/58a22bc9-4156-436d-9d11-87f986387377)<br>
  <p style="text-align: center;">Fig.06. Teste Augmented Dickey-Fuller </p><br>

  Nota: O teste de estacionaridade retornou que **os dados são estacionários**, sendo assim não precisaremos de suavização por diferenciação, de modo que, d=0. <br><br>
  06. Train/Test Split.<br><br>
  > Para os métodos estatísticos, a divisão ficou assim: O tamanho da data de treinamento ficou estabelecido em **751 registros** e os dados de teste ficaram em **30 registros**.<br>
  > Para aprendizado de máquina, a divisão ficoua ssim: <br>| Particao de Treinamento: 0 375 |<br>| Particao de Validação: 375 564 |<br>| Particao de Teste: 562 751 |<br><br>
  07. Modelo AUTO-ARIMA.<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/f1e66709-d847-446c-8be5-41db149db72c) <br>
  <p style="text-align: center;">Fig.07. Results Auto-Arima </p><br>
  Nota: O Auto-ARIMA indica que os melhores parâmetros são AR=6, MA=1 e Dif=0 (já que os dados são estacionários).<br><br>

  08. Modelo ARIMA.<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/900ed9db-5298-4171-a494-4eca01db2787)<br>
  <p style="text-align: center;">Fig.08. ARIMA </p><br>

  09. Modelo ARMA.<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/ead42195-71fa-4760-b123-737392ce16e5)
  <p style="text-align: center;">Fig.09. ARMA </p><br>

  10. Comparação dos Modelos.<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/d30f5ca4-00d5-4826-a455-82a3be308f93)
<p style="text-align: center;">Fig.10. Arima x Arma </p><br>
  Nota: O modelo Arima apresentou maior performance. Deve-se a que usa os mesmos parámetros facilitados pelo Auto-Arima. Já o modelo Arma está usando as primeiras combinações possíveis de AR e MA. <br><br>
  11. Análise dos Resíduos<br><br>

  ![image](https://github.com/DavidPanduro/time_series_sales_prediction/assets/45201867/4636f78c-3e75-47e1-b04b-f8aa14e49bb0)<br>
  <p style="text-align: center;">Fig.11. Arima x Arma </p><br><br>
  Nota: Tem pontos saindo do Intervalo de confiança, o que indica que ainda podemos modelar a série. <br><br>
  12. Modelo MultiLayer Perceptron (MLP).<br><br>

  ![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/2ec0ba47-c662-4541-a7ef-f3964a2e6b31)
<p style="text-align: center;">Fig.12. Parametros do MLP </p><br><br>

![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/27e6f41e-ee61-4209-8bc8-43042824ea63)
<p style="text-align: center;">Fig.13. Previsção com MLP - dados de treinamento</p><br><br>

  13. Conclusões.<br><br>
  
> **Mediante Métodos Estatísticos**, ARIMA tem se mostrado, escolheríamos ARIMA(6,0,1).<br>
> **Mediante Aprendizado de Máquina**, MLP conseguiu bons resultados gráficamente e em termos de métricas obteve umbom MAPE, mas deveríamos prestar atenção em melhorar o MSE.<br><br>
**Resultado Gráfico do MultiLayer Perceptron**
![image](https://github.com/DavidPanduro/time_series_prediction/assets/45201867/ffceec86-3403-4997-8b0d-5a2cef0d7033)
<p style="text-align: center;">Fig.14. Previsção com MLP - dados de validação</p><br><br>
  ** MAPE: 9,5% ** <br>
  ** MSE: 353082 ** <br>

  Nota: O Valor de MAPE chega ser um valor promissorio e alentador. Pelo contrário, o MSE ficou um valor muito grande, isso explica que em alguns pontos o modelo está errando demais, o que está penalizando o MSE do modelo.<br><br>

**_próximos passos_** Como próximos passos posso sugerir: 
> Análise dos dados para identificar os resíduos significantes que acabam afetando demais o modelo.<br>
> Tratamento de outliers via z-score ou IQR.<br>
> Executar mais um ciclo da modalgem.<br>
> Aplicar outro algoritmo para modelagem (SVR)<br>


# time_series_prediction
