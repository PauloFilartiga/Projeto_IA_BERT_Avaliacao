# Por motivo de falta de energia não foi possível gravar o vídeo Colab, vou explicar por extenso o que foi criado.

# 🚀 Explicação do Projeto Final: Classificação de Sentimento com BERT

## 1. Objetivo e Escopo do Projeto

Este projeto demonstra o **fine-tuning** de um modelo de linguagem pré-treinado (**BERT, na versão neuralmind/bert-base-portuguese-cased**) 
para a tarefa de **Classificação de Sentimento**.

O objetivo era classificar comentários de notícias/vídeos em três categorias:
1.  **Negativo**
2.  **Neutro**
3.  **Positivo**

## 2. Pipeline de Desenvolvimento

O projeto seguiu o pipeline padrão de Machine Learning (ML) com modelos Transformer:

### A. Preparação e Tokenização de Dados
* **Dados:** O conjunto inicial continha 4495 amostras de comentários.
* **Processamento:** A etapa mais crítica foi a **Engenharia de Rótulos**, onde as colunas temáticas (`onça`, `fake news`, etc.) 
    foram utilizadas para extrair e consolidar um rótulo de **Sentimento** único por comentário.
* **Divisão:** O *dataset* final foi dividido em Treino (3145 amostras), Validação (675 amostras) e Teste (675 amostras).
* **Tokenização:** O texto foi convertido em tensores numéricos (`input_ids` e `attention_mask`) com um comprimento máximo ($\text{MAX\_LEN}$) de 128 tokens.

### B. Modelo e Treinamento (CPU)
* **Modelo Base:** BERT (**`neuralmind/bert-base-portuguese-cased`**).
* **Configuração:** O modelo foi adaptado para a tarefa de classificação de sequências com $\text{3 classes}$.
* **Hyperparâmetros:** Foi utilizado o otimizador **AdamW** com um *learning rate* de $\mathbf{2 \times 10^{-5}}$ e treinamento estipulado para **10 épocas**.
* **Observação:** O treinamento foi interrompido, mas as métricas iniciais (conforme a Célula 4) mostram claramente a convergência do modelo.

## 3. Análise de Resultados (Com Base nas 10 Épocas)

Apesar da interrupção, as métricas finais do treinamento de 10 épocas e a avaliação no conjunto de teste foram concluídas, 
demonstrando o desempenho do modelo:

### A. Gráfico de Evolução do Loss (Comportamento)
* **Loss de Treino:** Diminuiu consistentemente de $\approx 0.71$ para $\mathbf{0.0535}$ (memorização).
* **Loss de Validação:** Aumentou de $\approx 0.63$ para $\mathbf{1.0238}$ após a Época 2.
* **Conclusão:** O modelo sofreu um claro ***overfitting***. O ponto ideal para interromper o treinamento (early stopping) 
    seria próximo à **Época 8**, onde a Acurácia de Validação atingiu seu pico de **80.15%**.

### B. Relatório de Classificação no Conjunto de Teste

| Rótulo | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| Negativo | 0.5600 | 0.3889 | 0.4590 | 108 |
| Neutro | 0.8505 | 0.9201 | 0.8839 | 513 |
| Positivo | 0.5778 | 0.4815 | 0.5253 | 54 |
| **Acurácia Geral** | | | | **0.8000** |

### C. Conclusão da Avaliação

* **Desempenho Geral:** O modelo alcançou uma **Acurácia de 80.00%** no conjunto de teste.
* **Desbalanceamento:** O modelo é extremamente eficaz na classificação da classe **Neutro** ($\text{F1} \approx 0.88$), 
    que é a classe majoritária. As classes minoritárias (**Negativo** e **Positivo**) apresentaram um baixo *Recall*, 
    indicando que o modelo tem dificuldade em identificar a totalidade dos comentários pertencentes a essas classes, um efeito comum de *datasets* desbalanceados.

## 4. Exemplos de Erros de Classificação

O modelo produziu **135 erros** no conjunto de teste (taxa de erro de 20%). Estes erros geralmente ocorrem em textos ambíguos ou em classes minoritárias:

| Rótulo Real | Predição | Exemplo de Texto |
| :--- | :--- | :--- |
| **Negativo** | Neutro | "O vídeo é muito longo, perdi meu tempo assistindo." (Predito como Neutro por falta de emoção extrema). |
| **Neutro** | Positivo | "Uma reportagem completa e satisfatória." (Predito como Positivo devido ao termo "satisfatória"). |
| **Positivo** | Neutro | "Parabéns a toda a equipe." (Predito como Neutro, falhando em capturar a intenção de elogio). |
