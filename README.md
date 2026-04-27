# Enterprise Challenge - Sprint 1 - DASA

# FIAP - Inteligência artificial e data science

<p align="center">
<a href= "https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Admnistração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# Nome do projeto
Cap 2 - Colheita de Dados e Insights - dados valiosos e maduros - Enterprise Challenge - Sprint 1

## Nome do grupo
39

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/company/inova-fusca">Guilherme Campos Hermanowski </a>
- <a href="https://www.linkedin.com/company/inova-fusca">Gabriel Viel </a>
- <a href="https://www.linkedin.com/company/inova-fusca"> Matheus Alboredo Soares</a> 
- <a href="https://www.linkedin.com/company/inova-fusca">Jonathan Willian Luft </a>

## 👩‍🏫 Professores:
### Tutor(a) 
- <a href="https://www.linkedin.com/company/inova-fusca">Leonardo Ruiz Orabona</a>
### Coordenador(a)
- <a href="https://www.linkedin.com/company/inova-fusca">ANDRÉ GODOI CHIOVATO</a>


## 📜 Justificativa do problema

Atualmente, relatórios e laudos médicos entregues aos pacientes após exames ou consultas são redigidos em uma linguagem altamente técnica, o que dificulta sua compreensão. Na maioria dos casos, os pacientes não possuem o conhecimento necessário para interpretar corretamente essas informações, o que gera dúvidas sobre seu próprio quadro clínico. Como consequência, torna-se necessária a intervenção de um profissional de saúde para esclarecer o conteúdo, contribuindo ainda mais para a sobrecarga já existente desses profissionais.

<br>

## 💡 2. A Solução

Diante desse cenário, propomos uma plataforma baseada em **RAG (Retrieval-Augmented Generation)**, que atua como uma ponte entre o conteúdo técnico dos documentos (como PDFs) e o entendimento do usuário. A solução vai além da simples extração de dados: ela contextualiza informações, explica possíveis riscos e sugere hábitos preventivos de forma clara, acessível e interativa.

<br>

### 👥 3. Perfis de Usuário (User Personas & Needs)

Para que a solução entregue valor real, mapeamos três perfis que interagem com os dados da Genera, cada um com objetivos distintos:

* **O Paciente (Leigo):**
    * **Necessidade:** Tradução de termos técnicos (ex: "polimorfismo", "variante") para uma linguagem cotidiana e acessível.
    * **O que busca:** Respostas práticas como "O que devo mudar na minha dieta?" ou "Qual o resumo do meu risco para doenças?".
* **O Médico (Especialista):**
    * **Necessidade:** Síntese e precisão. O profissional não dispõe de tempo para ler relatórios de 50 páginas durante a consulta.
    * **O que busca:** Um sumário executivo com biomarcadores alterados e níveis de evidência científica para embasar a conduta clínica.
* **O Analista de Dados (Dasa/Genera):**
    * **Necessidade:** Estruturação de dados para escala e inteligência de negócio.
    * **O que busca:** Transformar PDFs estáticos em dados tabulares para identificar tendências populacionais de saúde e melhorar o produto.

---

### 📊 4. Estruturação dos Dados (Modelo JSON)

Abaixo, apresentamos a proposta de como o motor de extração (ETL) converterá as informações desestruturadas do PDF em um objeto **JSON**. Esta estrutura é o "cérebro" que permite à IA realizar buscas rápidas e precisas através de RAG:

```json
{
  "metadados": {
    "paciente_id_hash": "a7b8c9d0...", 
    "data_relatorio": "2026-04-27",
    "versao_painel": "Genera Premium 3.0"
  },
  "blocos_de_conhecimento": [
    {
      "categoria": "Saúde e Bem-Estar",
      "topico": "Predisposição a Doenças",
      "detalhes": [
        {
          "condicao": "Diabetes Tipo 2",
          "risco_relativo": "Aumentado (1.8x)",
          "genes_impactados": ["TCF7L2", "KCNJ11"],
          "evidencia_cientifica": "Alta",
          "insight_ia": "Sugerir redução de ingestão de carboidratos simples e monitoramento de hemoglobina glicada."
        }
      ]
    },
    {
      "categoria": "Ancestralidade",
      "composicao": [
        { "regiao": "Europa Ocidental", "percentual": 58.4 },
        { "regiao": "Nativo Americano", "percentual": 12.2 }
      ]
    },
    {
      "categoria": "Farmacogenética",
      "medicamentos": [
        {
          "principio_ativo": "Varfarina",
          "metabolismo": "Lento",
          "alerta": "Risco aumentado de toxicidade; ajuste de dose necessário."
        }
      ]
    }
  ]
}
```


## 🔧 5. Arquitetura e Pipeline

O fluxo de processamento segue o pipeline abaixo:

- **5.1.  Ingestão:** Upload do arquivo PDF (Relatório Genera).

- **5.2.  Extração (ETL):** Processamento do documento via bibliotecas de extração de texto e tabelas (ex: PyMuPDF/Camelot).

- **5.3.  *Estruturação:** Conversão dos dados não estruturados para formato **JSON**, categorizando riscos, genes e recomendações.

- **5.4.  IA e RAG:**
     * **Embeddings:** Fragmentação e vetorização dos dados.
     * **Vector DB:** Armazenamento para busca semântica.

- **5.5.  Interface:** Chatbot interativo que utiliza uma LLM para responder às dúvidas do usuário com base no contexto do seu DNA.


## 🔧 Funcionamento

O sistema utiliza uma arquitetura de monitoramento inteligente na AWS, integrando sensores físicos, banco de dados, machine learning e notificações automatizadas. O ESP32 envia dados de sensores (volume de produção, temperatura, umidade e vibração) via MQTT para o AWS IoT Core, com comunicação segura por TLS e autenticação por certificados. Esses dados são roteados para uma função AWS Lambda, que grava as informações no Amazon RDS, um banco relacional gerenciado e seguro.

Para viabilizar análises futuras e separar a carga operacional da base produtiva, os dados do RDS são exportados para o Amazon S3. Esse armazenamento forma o Data Lake, com controle de acesso gerenciado pelo AWS Lake Formation. A chegada de novos dados no S3 aciona automaticamente uma função AWS Lambda (via gatilho), que faz o pré-processamento utilizando Python e bibliotecas como pandas e boto3, e em seguida envia os dados ao Amazon SageMaker.

O Amazon SageMaker realiza a inferência com modelos desenvolvidos em Python, utilizando bibliotecas como TensorFlow, scikit-learn, numpy e pandas, para detectar padrões e antecipar possíveis falhas operacionais. Os resultados podem ser armazenados no RDS ou encaminhados a outras funções Lambda para tomada de decisão.

Workflows mais complexos e decisões condicionais são coordenados por AWS Step Functions, que orquestram a sequência de chamadas e ações de forma estruturada.

Para observabilidade, o Amazon CloudWatch coleta métricas e logs de todos os serviços envolvidos, como Lambda, SageMaker e Step Functions. Alarmes podem ser configurados para detectar falhas, tempos de resposta anormais ou comportamentos críticos, acionando o Amazon SNS para notificar os responsáveis via e-mail, SMS ou integração com sistemas externos.

## 👨‍🎓 Divisão de responsabilidades:
- Arquitetura (Pipeline e estrutura de features na AWS) : <a href="https://www.linkedin.com/company/inova-fusca">Gabriel Viel </a>
- Coleta de dados: <a href="https://www.linkedin.com/company/inova-fusca">Jonathan Willian Luft </a> e <a href="https://www.linkedin.com/company/inova-fusca">Guilherme  Campos Hermanowski </a>
- Banco de Dados: <a href="https://www.linkedin.com/company/inova-fusca">Gabriel Viel </a>
- Treinamento de IA: <a href="https://www.linkedin.com/company/inova-fusca"> Matheus Alboredo Soares</a> 
- Integração de Features: <a href="https://www.linkedin.com/company/inova-fusca">Gabriel Viel </a>, <a href="https://www.linkedin.com/company/inova-fusca"> Matheus Alboredo Soares</a>, <a href="https://www.linkedin.com/company/inova-fusca">Jonathan Willian Luft </a> e <a href="https://www.linkedin.com/company/inova-fusca">Guilherme  Campos Hermanowski </a>



## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>
