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


## 📜 Justificativa do problema e descrição da solução proposta

<br>
Atualmente, relatórios e laudos médicos entregues aos pacientes após exames ou consultas são redigidos em uma linguagem altamente técnica, o que dificulta sua compreensão. Na maioria dos casos, os pacientes não possuem o conhecimento necessário para interpretar corretamente essas informações, o que gera dúvidas sobre seu próprio quadro clínico. Como consequência, torna-se necessária a intervenção de um profissional de saúde para esclarecer o conteúdo, contribuindo ainda mais para a sobrecarga já existente desses profissionais.

</p>

Diante desse cenário, propomos uma plataforma baseada em **RAG (Retrieval-Augmented Generation)**, que atua como uma ponte entre o conteúdo técnico dos documentos (como PDFs) e o entendimento do usuário. A solução vai além da simples extração de dados: ela contextualiza informações, explica possíveis riscos e sugere hábitos preventivos de forma clara, acessível e interativa.

</p>

## 🔧 Componentes

  -	***Funcionamento:*** Se a inferência do SageMaker indicar uma condição anormal, o Lambda ou Step Function publica uma mensagem no SNS que é entregue ao responsável via email, sms ou por alguma aplicação.<br>


## 📁 Arquitetura e Pipeline

![Pipeline AWS](https://github.com/user-attachments/assets/5eab299f-b2ad-4ea4-81e9-da8b4054551b)




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
