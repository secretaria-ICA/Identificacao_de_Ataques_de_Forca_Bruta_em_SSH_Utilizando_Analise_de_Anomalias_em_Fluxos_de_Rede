# Identificação de Ataques de Força Bruta em SSH Utilizando Análise de Anomalias em Fluxos de Rede (Netflow)

#### Aluno: Pedro Miguel Esposito (https://github.com/pmesposito)
#### Orientador: Leonardo Forero Mendoza

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/pmesposito/neflow_anomaly). 


---

### Resumo

Este projeto tem como objetivo utilizar de técnicas de análise de anomalias na identificação de ataques de força bruta, ou seja, situações em que o atacante tenta descobrir as credenciais de acesso a um serviço ou sistema através de tentativa e erro. Foi utilizada uma base de dados de fluxos de rede (netflow), que registra, para cada conexão, dados como ip de origem e de destino, porta de origem e de destino, número de pacotes e de bytes trafegados, duração e data/hora de início. Dessa base, selecionamos para análise os fluxos que utilizaram o protocolo SSH e que tiveram a participação de uma máquina de usuário final.

Ataques de força bruta podem ser caracterizados por tráfego de rede "flat", ou seja, que possui muitos registros similares devido às diversas tentativas de acesso negadas. Foi proposto na literatura que, em ataques SSH, as tentativas de acesso possuem tipicamente de 11 a 51 pacotes por fluxo, números que utilizamos para restringir ainda mais os registros selecionados. Agrupamos os fluxos em janelas temporais, como proposto pelo KDD Cup 1999. Essas janelas permitiram gerar novos atributos importantes, como o número de fluxos com a mesma origem e destino e o número de pacotes mais frequente (moda).

Foram avaliados diversos modelos não supervisionados de análise de anomalias, como o K-Nearest Neighbors (KNN), Local Outlier Factor (LOF), One-Class SVM e Isolation Forest. Os modelos não supervisionados se diferenciam de duas outras abordagens tradicionais utilizadas para a identificação de ataques: o aprendizado supervisionado e regras pré-definidas. Em relação ao aprendizado supervisionado, a análise não supervisionada se destaca por não necessitar de exemplos prévios da classe de interesse (no caso, ataques), que são de difícil obtenção em cenários reais. Regras pré-definidas, por sua vez, podem funcionar em muitos casos, porém são facilmente contornáveis pelos atacantes e podem ser tornar defasadas rapidamente. Além disso, a análise não supervisionada tem a capacidade de identificar novas formas de ataque que não foram previstas anteriormente.

Após avaliação qualitativa dos resultados, identificamos que os modelos baseados em proximidade (KNN e LOF) tiveram desempenho superior, permitindo destacar corretamente os outliers nos dados em estudo. Cabe ressaltar que, na abordagem não supervisionada, é necessário que cada registro destacado como anomalia seja enviado para especialistas, para que investiguem o evento em questão e decidam se ele é um falso positivo ou se representa um ataque real.

Referências:

- Flow-based Compromise Detection, Rick Hofstede, 2016, disponível em https://research.utwente.nl/files/6028286/thesis_R_Hofstede.pdf.
- KDD Cup 1999 Data, The UCI KDD Archive, 1999, disponível em http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html.
- Extracting Salient Features for Network Intrusion Detection Using Machine Learning Methods, Ralf C. Staudemeyer e Christian W. Omlinz, 2014, disponível em https://sacj.cs.uct.ac.za/index.php/sacj/article/view/200/99.
- Outlier Analysis, Charu C. Aggrarwal, 2016.

---

Matrícula: 192.671.128

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
