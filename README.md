# Projeto_IA_BERT_Avaliacao

# 🎯 Classificação em Comentários de Notícias (BERT-PT)

## 🚀 Visão Geral do Projeto
Este projeto implementa o fine-tuning do modelo BERT (neuralmind/bert-base-portuguese-cased) para classificar comentários de notícias em três categorias de sentimento: **Negativo**, **Neutro** e **Positivo**.

## 🗂️ Estrutura do Repositório
- **`notebooks/`**: Contém o notebook principal com todo o código de ETL, treinamento e avaliação.
- **`requirements.txt`**: Lista as dependências necessárias.
- **`README.md`**: Documentação do projeto e resultados.

## ⚙️ Configuração e Treinamento
- **Modelo Base:** `neuralmind/bert-base-portuguese-cased`
- **Dataset:** 4495 amostras (após filtragem e limpeza).
- **Hyperparâmetros:** Learning Rate = 2e-5, Optimizer = AdamW, Épocas = 10.

## 📈 Resultados da Avaliação (Conjunto de Teste)

O modelo atingiu uma **Acurácia Geral de 80.00%** no conjunto de teste.

### Relatório de Classificação

| Rótulo | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- |
| Negativo | 0.5600 | 0.3889 | 0.4590 |
| Neutro | 0.8505 | 0.9201 | 0.8839 |
| Positivo | 0.5778 | 0.4815 | 0.5253 |

### Análise
A métrica **F1-score** demonstra que o modelo é altamente eficaz na identificação de comentários **Neutros** (0.8839), que é a classe majoritária. As classes minoritárias (Negativo e Positivo) mostram um recall mais baixo, indicando um viés do modelo para a classe dominante devido ao desbalanceamento de dados.

![Google Drive](https://img.shields.io/badge/Google%20Drive-4285F4?style=for-the-badge&logo=googledrive&logoColor=white) [Arquivos do Google Drive (Meu Drive/Colab Notebooks)](https://drive.google.com/drive/u/1/folders/15bdEybB6ZRBDVx46LRxdSdTpMPg2eEfn)

![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white) [Link para o Vídeo de Explicação no YouTube]
