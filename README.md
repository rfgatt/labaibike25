# labaibike25
# 🚲 Previsão de Aluguel de Bicicletas com AutoML no Azure

Este projeto utiliza o **Automated Machine Learning (AutoML) no Azure Machine Learning** para treinar e implantar um modelo de previsão de aluguel de bicicletas com base em dados meteorológicos e sazonais.

---

## 🎯 Objetivo
Criar e implantar um modelo de **regressão** que prevê a quantidade esperada de bicicletas alugadas em um determinado dia.

---

## 📊 Dataset
Utilizamos um dataset de históricos de aluguel de bicicletas. O dataset contém informações como:
- Dia, mês e ano
- Condições meteorológicas (temperatura, umidade, vento)
- Dia da semana e feriados
- Número de bicicletas alugadas

Fonte: [Capital Bikeshare](https://aka.ms/bike-rentals)

---

## 🚀 Etapas do Projeto

1️⃣ **Criação do Ambiente no Azure**
- Criamos um workspace no Azure Machine Learning.  
- Configuramos o armazenamento (Blob Storage) e chaves de segurança (Key Vault).  

2️⃣ **Configuração do AutoML**
- Criamos um **experimento chamado `mslearn-bike-rental`**.  
- Escolhemos a **tarefa de Regressão** e o dataset `bike-rentals`.  
- Configuramos os parâmetros:
  - **Modelos testados**: RandomForest, LightGBM.
  - **Métrica principal**: NormalizedRootMeanSquaredError.
  - **Validação**: 10% dos dados.
  - **Máximo de 3 execuções simultâneas**.

3️⃣ **Treinamento e Avaliação do Modelo**
- O melhor modelo identificado foi `LightGBM`.
- Avaliação do modelo baseada em:
  - **Erro normalizado**: `0.085`
  - **Resíduos e gráficos de comparação predito x real**.

4️⃣ **Implantação do Modelo**
- Criamos um **endpoint de inferência em tempo real**.
- Configuração do deployment:
  - VM: `Standard_DS3_v2` com 3 instâncias.
  - Método: **Azure Container Instance**.

---

## 🧪 Testando a API do Modelo

### **Exemplo de Entrada (JSON)**
Para testar a API no Azure Machine Learning Studio:

```json
{
  "input_data": {
    "columns": [
      "day",
      "mnth",
      "year",
      "season",
      "holiday",
      "weekday",
      "workingday",
      "weathersit",
      "temp",
      "atemp",
      "hum",
      "windspeed"
    ],
    "index": [0],
    "data": [[1,1,2022,2,0,1,1,2,0.3,0.3,0.3,0.3]]
  }
}
