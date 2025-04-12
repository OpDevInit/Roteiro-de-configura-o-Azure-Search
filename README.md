# Azure Cognitive Search: Configuração de Pesquisa e Análise de Sentimentos

Este repositório descreve o processo de configuração do **Azure Cognitive Search**, integrando análise de sentimentos e realizando pesquisas eficientes com base em grandes volumes de dados não estruturados. O processo inclui a criação do serviço, configuração do índice de pesquisa, importação de dados, uso de habilidades cognitivas e execução de pesquisas, além dos insights adquiridos ao longo do processo.

## Passo 1: Criar Conta e Configurar o Serviço no Azure

1. **Criar uma Conta no Azure**:
   - Acesse o [portal do Azure](https://portal.azure.com/) e crie uma conta, se ainda não tiver uma.

2. **Criar o Serviço Azure Cognitive Search**:
   - No portal do Azure, clique em **Criar um recurso** e busque por **Azure Cognitive Search**.
   - Preencha os campos necessários, como nome do serviço, grupo de recursos e região.
   - Após a criação, obtenha a **chave de acesso** na seção **Chaves de Acesso** do painel de configurações do serviço.



## Passo 2: Criar e Configurar o Índice de Pesquisa

O índice define como seus dados serão estruturados e pesquisados. Nele, você define os campos que serão pesquisados, como texto, números e outras informações.

1. **Definir o Índice**:
   - No painel de **Índices** do Azure Cognitive Search, crie um novo índice e defina os campos que serão indexados.
   
     Exemplo de definição de índice:

     ```json
     {
       "name": "feedback-index",
       "fields": [
         { "name": "id", "type": "Edm.String", "key": true, "retrievable": true },
         { "name": "text", "type": "Edm.String", "retrievable": true },
         { "name": "sentiment", "type": "Edm.String", "retrievable": true }
       ]
     }
     ```

2. **Características dos Campos**:
   - **Key**: Campo chave primária, que identifica unicamente o documento.
   - **Searchable**: Campo que será incluído nas consultas de pesquisa.
   - **Retrievable**: Campo que será retornado nos resultados da pesquisa.

## Passo 3: Importar Dados para o Índice

Agora, é hora de alimentar o índice com os dados. Você pode usar fontes de dados como **Azure Blob Storage**, **SQL Database** ou adicionar os dados manualmente via API.

1. **Importação Manual de Dados**:
   - Se você deseja adicionar dados diretamente, use a API de **Upload de Documentos**.

     Exemplo de dados a serem adicionados:

     ```json
     {
       "value": [
         {
           "@search.action": "upload",
           "id": "1",
           "text": "Eu adoro o serviço de Azure, é fantástico!",
           "sentiment": "positivo"
         },
         {
           "@search.action": "upload",
           "id": "2",
           "text": "O desempenho é bom, mas pode melhorar.",
           "sentiment": "neutro"
         }
       ]
     }
     ```

2. **Usar Indexers**:
   - Se os dados estiverem em fontes como bancos de dados ou armazenamento de blobs, configure um **indexer** para automatizar a importação.

## Passo 4: Integrar Habilidades Cognitivas

Você pode adicionar **habilidades cognitivas** ao pipeline de indexação, como **análise de sentimentos** e **extração de texto**, para enriquecer seus dados.

1. **Criar um Skillset**:
   - No portal do Azure, crie um **Skillset** e adicione habilidades de **Text Analytics**, como análise de sentimentos.
   
2. **Adicionar ao Indexer**:
   - Adicione o **Skillset** ao seu indexer para que as habilidades sejam aplicadas durante a indexação.


## Passo 5: Realizar Pesquisas

Agora que o índice está configurado e os dados foram importados, você pode começar a realizar pesquisas.

1. **Pesquisa Simples**:
   - Realize uma pesquisa simples procurando por palavras-chave ou frases específicas.

     Exemplo de consulta via API:

     ```bash
     GET https://<seu-endpoint>.search.windows.net/indexes/feedback-index/docs?search=Azure&api-version=2021-04-30-Preview
     ```

2. **Pesquisa com Filtros**:
   - Use filtros para refinar os resultados com base em campos específicos, como o **sentimento**.

     Exemplo de consulta com filtro de sentimento:

     ```bash
     GET https://<seu-endpoint>.search.windows.net/indexes/feedback-index/docs?search=Azure&$filter=sentiment eq 'positivo'&api-version=2021-04-30-Preview
     ```

## Passo 6: Monitoramento e Ajustes

Após configurar o sistema de pesquisa, é importante monitorar a performance das consultas e ajustar conforme necessário.

1. **Monitoramento de Uso**:
   - Utilize os recursos de **monitoramento** do Azure para acompanhar o uso de recursos e desempenho das consultas.

2. **Ajustes no Índice**:
   - Com base nos feedbacks e resultados, ajuste os campos do índice ou a configuração das habilidades para melhorar os resultados da pesquisa.

## Ferramentas que se Beneficiam do Azure Cognitive Search

- **Sistemas de Recomendação**: Usando dados indexados e habilidades cognitivas, você pode oferecer recomendações personalizadas em tempo real.
- **Plataformas de Feedback de Clientes**: Analise automaticamente o feedback de clientes, categorizando-os com base em sentimentos para facilitar respostas rápidas.
- **Aplicações Web e Móveis**: Qualquer aplicativo que precise oferecer uma experiência de busca poderosa e personalizada pode se beneficiar do Azure Cognitive Search.

---

## Conclusão

Ao configurar o **Azure Cognitive Search**, você ganha a capacidade de realizar pesquisas poderosas em grandes volumes de dados, com a adição de habilidades cognitivas para enriquecer as informações. A capacidade de realizar pesquisas refinadas com base em sentimentos e outros critérios ajuda a melhorar a relevância dos resultados e oferece insights valiosos.

**Aprendizados principais**:
- Planejar adequadamente os índices e escolher os tipos de dados corretos para otimizar as pesquisas.
- Usar habilidades cognitivas para enriquecer os dados e melhorar a precisão das consultas.
- Monitorar continuamente o desempenho da pesquisa e ajustar conforme necessário para garantir a eficiência e reduzir custos.

Agora você está pronto para explorar o Azure Cognitive Search e aproveitar suas capacidades de pesquisa avançada para criar soluções poderosas!
