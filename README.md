# ✍️ Signature Recognizer

**Implementação de um sistema de verificação de similaridade de assinaturas utilizando redes neurais e Triplet Loss, com foco em embeddings, avaliação biométrica e o dataset CEDAR.**

[![Licença](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-3.4.1-green.svg)]()
[![Status](https://img.shields.io/badge/status-concluído-greend.svg)]()
[![deploy](https://img.shields.io/badge/depoly-inactive-red.svg)]()


## 📌 Sumário

1.  [Sobre o Projeto](https://www.google.com/search?q=%23-sobre-o-projeto)
2.  [Objetivos](https://www.google.com/search?q=%23-objetivos)
3.  [Tecnologias](https://www.google.com/search?q=%23-tecnologias)
4.  [Funcionalidades](https://www.google.com/search?q=%23-funcionalidades)
5.  [Pré-requisitos](https://www.google.com/search?q=%23%25EF%25B8%258F-pr%C3%A9-requisitos)
6.  [Instalação](https://www.google.com/search?q=%23%25EF%25B8%258F-instala%C3%A7%C3%A3o)
7.  [Como utilizar](https://www.google.com/search?q=%23-como-utilizar)
8.  [Estrutura do Projeto](https://www.google.com/search?q=%23-estrutura-do-projeto)
9.  [Contribuição](https://www.google.com/search?q=%23-contribui%C3%A7%C3%A3o)
10. [Licença](https://www.google.com/search?q=%23-licen%C3%A7a)
11. [Contato](https://www.google.com/search?q=%23-contato)
12. [Recursos Adicionais](https://www.google.com/search?q=%23-recursos-adicionais)

## 💻 Sobre o Projeto

O projeto **"Signature Recognizer"** representa a **Fase de Protótipo** do nosso sistema de verificação de similaridade, aplicando os conceitos de redes siamesas com **Triplet Loss** ao domínio de **assinaturas manuscritas**. Após validação inicial no dataset MNIST no nosso software anterior [*Seamese networks algorithm*](https://github.com/lucasgleria/seamese-network-algorithm), focamos agora no desafiador **dataset CEDAR**, que contém assinaturas genuínas e forjadas.

A essência do projeto é treinar uma rede neural profunda para gerar **embeddings** (vetores de características) para assinaturas. O objetivo é que assinaturas genuínas do mesmo indivíduo resultem em embeddings muito próximos no espaço vetorial, enquanto assinaturas forjadas (ou de outros indivíduos) gerem embeddings distantes. Isso permite que, dada uma assinatura de "consulta", possamos verificar sua autenticidade comparando-a com um conjunto de referências.

  - *Motivação*: Desenvolver um protótipo funcional para a verificação automatizada de assinaturas, um desafio significativo em áreas como segurança e autenticação.
  - *Público-alvo*: Estudantes, pesquisadores e desenvolvedores interessados em Deep Learning, Visão Computacional, Biometria e Sistemas de Segurança.

## 🎯 Objetivos

### 🛠️ Técnicos

  - Adaptar a pipeline de dados para processar o **dataset CEDAR**, incluindo pré-processamento específico para imagens de assinatura (binarização, redimensionamento).
  - Treinar o modelo **EfficientNet-B0** com **Triplet Loss** utilizando triplets de assinaturas (Anchor, Positive, Negative) do CEDAR.
  - Implementar funcionalidades para **gerar embeddings** de todas as assinaturas genuínas e forjadas.
  - Desenvolver uma função de **verificação de assinatura** baseada na distância euclidiana entre embeddings.
  - Avaliar o desempenho do sistema utilizando métricas biométricas padrão, como a **Curva ROC** e o **Equal Error Rate (EER)**, para otimizar o limiar de decisão.
  - Fornecer um **ambiente de execução configurável** no Google Colab, facilitando a reprodução e experimentação do protótipo.

## 🚀 Tecnologias

**Núcleo do Sistema**

  - **Python**: Linguagem de programação principal.
  - **PyTorch**: Framework de Deep Learning para construção e treinamento do modelo.
  - **torchvision**: Pacote do PyTorch para datasets e transformações de visão.
  - **timm (PyTorch Image Models)**: Biblioteca essencial para modelos pré-treinados (EfficientNet-B0).
  - **scikit-image**: Para operações de pré-processamento de imagens (binarização, conversão de cor, redimensionamento).
  - **scikit-learn**: Para cálculo de métricas de avaliação (ROC, AUC) e suporte a funções matemáticas.
  - **NumPy**: Para operações numéricas e manipulação de arrays.
  - **Pandas**: Para manipulação e análise de DataFrames (metadados e embeddings).
  - **Matplotlib**: Para visualização de imagens, curvas ROC e resultados.
  - **Google Colab**: Ambiente de desenvolvimento e execução ideal.

## ✨ Funcionalidades

  - ✅ **Preparação do Ambiente**: Instalação automática de bibliotecas necessárias e configuração de parâmetros globais (`BATCH_SIZE`, `LR`, `EPOCHS`, `DEVICE`, `IMAGE_SIZE`).
  - ✅ **Download e Preparação do Dataset CEDAR**: Automação do download, descompactação e estruturação do dataset CEDAR.
  - ✅ **Geração de Triplets Adaptada**: Lógica para criar amostras Triplet (Anchor, Positive, Negative) especificamente para assinaturas do CEDAR, garantindo a diversidade de classes e a representatividade.
  - ✅ **Pré-processamento de Imagens de Assinatura**: Implementação de pipeline de pré-processamento que inclui conversão para escala de cinza, binarização por Otsu e redimensionamento para adequação ao modelo.
  - ✅ **Modelo de Embeddings Robusto**: Utilização do **EfficientNet-B0** pré-treinado como *backbone*, ajustado para gerar vetores de embedding de alta qualidade para assinaturas.
  - ✅ **Treinamento com Triplet Loss**: Implementação eficaz das funções de treinamento e avaliação com a `nn.TripletMarginLoss`, focando na convergência do modelo para embeddings discriminativos.
  - ✅ **Salvar Melhor Modelo**: Mecanismo para persistir os pesos do modelo que demonstra a melhor performance no conjunto de validação, permitindo sua reutilização.
  - ✅ **Geração de Embeddings para Inferência**: Funções otimizadas para gerar embeddings para um grande conjunto de assinaturas (genuínas e forjadas) para construção de um banco de dados de referência.
  - ✅ **Verificação de Assinatura**: Função central para verificar a autenticidade de uma assinatura de consulta comparando-a com referências usando **distância euclidiana** e um limiar.
  - ✅ **Avaliação de Desempenho Biométrico**: Cálculo da **Curva ROC** e do **Equal Error Rate (EER)**, fornecendo métricas quantitativas do desempenho do sistema e um limiar de decisão otimizado.
  - ✅ **Visualização de Curva ROC**: Plotagem da Curva ROC e do ponto EER para análise visual da performance do sistema.

## ⚙️ Pré-requisitos

  - **Acesso ao Google Colab**: O projeto é otimizado para execução neste ambiente, aproveitando a aceleração por GPU.
  - **Conexão estável à internet**: Necessária para baixar bibliotecas e o dataset CEDAR.
  - **Conhecimentos básicos de Python e PyTorch**: Para entender e, se desejar, modificar o código e a lógica do protótipo.

## 🛠️ Instalação

Como este projeto é idealmente executado no Google Colab, a "instalação" se resume a abrir o notebook e executar as células em sequência.

1.  **Abra o notebook no Google Colab:**
    Clique no ícone "Open in Colab" no topo deste README ou acesse diretamente o link: ```https://colab.research.google.com/drive/1DGfyOQH44typ2CT6g8NYBxTUd_SI-aa0?usp=sharing```

2.  **Execute as células:**
    Siga a ordem das seções no notebook Colab. As células contêm os comandos de instalação de bibliotecas (`!pip install...`), o download e preparação do dataset, e todo o código-fonte necessário para o projeto.

## ❗ Como Utilizar

Após executar todas as células do notebook Google Colab:

1.  **Configuração e Ambiente**: A primeira seção configurará o ambiente, instalará as dependências e definirá as constantes globais.
2.  **Preparação de Dados**: As células subsequentes realizarão o download e a preparação do dataset CEDAR, incluindo a crucial etapa de geração dos triplets de assinaturas.
3.  **Treinamento do Modelo**: A seção de treinamento iniciará o processo de aprendizado do modelo EfficientNet-B0 com a Triplet Loss, exibindo o progresso por épocas e salvando o melhor modelo encontrado.
4.  **Geração de Embeddings e Verificação**: Após o treinamento, o modelo será usado para gerar embeddings para as assinaturas. Em seguida, a função `verify_signature` demonstrará como uma assinatura pode ser autenticada (ou rejeitada) comparando-a com referências.
5.  **Avaliação de Desempenho**: A última seção calculará e plotará a Curva ROC e o EER, fornecendo uma visão quantitativa do desempenho do sistema e o limiar de decisão otimizado. Você verá como este limiar pode ser aplicado na verificação.

### ▶️ Demonstração

![Signature](https://media.tenor.com/kO2TfoN8bnUAAAAM/waiver-sighn.gif)

*(Gif meramente ilustrativo)*

## 📂 Estrutura do Projeto

O projeto é contido principalmente em um único notebook Google Colab, estruturado em seções lógicas para facilitar a compreensão do fluxo e a depuração:

```plaintext
├── signature_recognizer.ipynb  # O notebook principal do Google Colab
├── LICENSE                     # LICENSE
└── README.md                   # Este arquivo
```

## 🤝 Contribuição

Contribuições são bem-vindas\! Se você tiver ideias para melhorias, novas funcionalidades ou encontrar algum bug, sinta-se à vontade para:

1.  **Reportar bugs**: Abra uma [issue](https://www.google.com/search?q=https://github.com/lucasgleria/signature-recognizer/issues) no GitHub.
2.  **Sugira melhorias**: Envie ideias ou *pull requests* com novas funcionalidades.
3.  **Desenvolva**:
      - Faça um *fork* do repositório.
      - Crie uma nova *branch* (`git checkout -b feature/sua-funcionalidade`).
      - Implemente suas alterações e faça os *commits*.
      - Envie um *Pull Request* detalhando suas modificações.

## 📜 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 📞 Contato & Evidências

  - **Autor**: [Lucas Leria](https://github.com/lucasgleria)
  - **LinkedIn**: [lucasgleria](https://www.linkedin.com/in/lucasgleria/)

## 🔍 Recursos Adicionais

  - [Documentação Oficial do PyTorch](https://pytorch.org/docs/stable/index.html)
  - [Documentação Oficial do timm](https://www.google.com/search?q=https://rwightman.github.io/pytorch-image-models/README/)
  - [Dataset CEDAR](https://www.kaggle.com/datasets/shreelakshmigp/cedardataset)