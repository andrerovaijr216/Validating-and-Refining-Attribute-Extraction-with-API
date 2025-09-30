# Sprint 3: Extração de Atributos de Cartuchos de Impressora com LLaVA

## 🚩 Sobre o Projeto

Este projeto é um protótipo desenvolvido para a Sprint 3 com o objetivo de analisar imagens de cartuchos e toners de impressora e extrair atributos relevantes de forma automatizada. Utilizando o poder do modelo multimodal open-source **LLaVA (Large Language and Vision Assistant)**, o sistema processa imagens a partir de URLs, identifica características-chave e estrutura os dados de saída em um arquivo CSV.

O núcleo da solução reside na engenharia de prompts, onde um prompt detalhado instrui o modelo a agir como um especialista em suprimentos de impressora e a retornar os dados em um formato JSON estruturado, garantindo a consistência e a facilidade de parsing dos resultados.

## 👥 Equipe

| Nome | RM |
| :--- | :--- |
| André Rovai | RM555848 |
| Thiago Almança | RM558108 |
| Alan de Souza | RM557088 |
| Leonardo Zago | RM558691 |
| Renan de França | RM558413 |
| Antonio Vinicius | RM558014 |

## ✨ Funcionalidades

*   **Extração Multimodal:** Analisa imagens para extrair informações textuais e visuais.
*   **Atributos-Alvo:** Focado em extrair o modelo do cartucho, tipo (Original, Compatível), cor e a presença de selo de autenticidade.
*   **Engenharia de Prompts:** Utiliza um prompt bem definido para guiar o modelo e formatar a saída em JSON.
*   **Processamento em Lote:** Capaz de processar uma lista de imagens a partir de suas URLs.
*   **Saída Estruturada:** Salva os resultados de forma organizada em um arquivo `.csv` para fácil análise e utilização.

## 🛠️ Tecnologias Utilizadas

O projeto foi construído utilizando as seguintes tecnologias:

*   **Python 3**
*   **Jupyter Notebook (Google Colab)**
*   **Modelo Multimodal:** `llava-hf/llava-1.5-7b-hf`
*   **Bibliotecas Principais:**
    *   `transformers`: Para carregar e interagir com o modelo LLaVA.
    *   `torch`: Backend de deep learning.
    *   `bitsandbytes`: Para quantização do modelo em 4-bit, permitindo a execução em GPUs com menos VRAM.
    *   `accelerate`: Para otimizar a execução do PyTorch.
    *   `pandas`: Para manipulação e armazenamento dos dados extraídos.
    *   `Pillow`: Para processamento de imagens.

## ⚙️ Configuração e Instalação

Para executar este projeto, é altamente recomendável utilizar um ambiente com GPU, como o Google Colab, pois o modelo LLaVA requer aceleração de hardware.

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/seu-usuario/nome-do-repositorio.git
    cd nome-do-repositorio
    ```

2.  **Instale as Dependências:**
    O notebook já inclui o comando de instalação. Execute a primeira célula de código para instalar todas as bibliotecas necessárias:
    ```python
    !pip install transformers torch bitsandbytes accelerate Pillow -q
    ```

## ▶️ Como Executar

1.  **Abra o Notebook:**
    Carregue o arquivo `Validating_and_Refining_Attribute_Extraction_with_API (1).ipynb` em um ambiente Jupyter, preferencialmente o Google Colab com um runtime de GPU habilitado (a GPU Tesla T4 foi utilizada no desenvolvimento).

2.  **Execute as Células:**
    Execute as células do notebook em ordem sequencial. O script irá:
    *   Instalar as dependências.
    *   Carregar o modelo LLaVA 1.5 de 7 bilhões de parâmetros com quantização de 4-bit.
    *   Definir a lista de imagens de cartuchos a serem processadas.
    *   Executar a função de extração para cada imagem.
    *   Processar as respostas em JSON, tratar possíveis erros e organizar os dados.
    *   Salvar os resultados no arquivo `extracao_atributos_llava_v5.csv`.
    *   Exibir a tabela final de resultados.

## 📈 Resultados

Após a execução, o script gerou o seguinte arquivo CSV (`extracao_atributos_llava_v5.csv`), demonstrando a capacidade do modelo em extrair os atributos solicitados:

| nome\_imagem | url\_imagem | modelo\_cartucho | tipo\_cartucho | cor | selo\_original\_presente |
| :--- | :--- | :--- | :--- | :--- | :--- |
| hp\_664\_preto\_original.jpg | `https://fotos.oceanob2b.com/High/035033.jpg` | Não identificado | Compatível | Preto | False |
| toner\_brother\_tn2370\_compativel.jpg | `https://img.kalunga.com.br/fotosdeprodutos/217715z_1.jpg` | TN2370 | Compatível | Preto | True |
| epson\_t544\_preto\_original.jpg | `https://images.tcdn.com.br/img/...` | Epson 544 | Original | Preto | True |
| canon\_cl246\_colorido\_original.jpg | `https://m.media-amazon.com/images/I/71xOF3-NTjL.jpg` | Canon | Original | Colorido | True |
| hp\_954\_amarelo\_compativel.png | `https://br-media.hptiendaenlinea.com/catalog/...` | Não identificado | Compatível | Não identificado | False |

### Análise dos Resultados

O modelo demonstrou sucesso na extração da maioria dos atributos. No entanto, houve desafios em identificar o "modelo do cartucho" e a "cor" em imagens onde essa informação não estava proeminente ou clara. Isso destaca a importância da qualidade da imagem e da contínua necessidade de refinar os prompts para melhorar a precisão em casos mais ambíguos.
