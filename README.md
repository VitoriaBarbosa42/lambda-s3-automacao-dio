# Automação com Lambda Function e S3

Este projeto foi desenvolvido como parte do desafio da DIO com o objetivo de consolidar os conhecimentos em tarefas automatizadas utilizando AWS Lambda Function e Amazon S3. A solução criada demonstra como um evento de upload de arquivo em um bucket S3 pode acionar automaticamente uma função Lambda para processar o objeto.

A documentação a seguir detalha a arquitetura, o processo de implementação e os aprendizados adquiridos durante o desafio.

### Arquitetura da Solução

Amazon S3 (Simple Storage Service): Um bucket S3 foi configurado para armazenar os arquivos de entrada.

AWS Lambda: Uma função Lambda foi criada e configurada com a permissão necessária para ser acionada pelo S3.

Gatilho (Trigger): Um gatilho foi estabelecido no bucket S3, de modo que toda vez que um novo objeto é adicionado, ele envia uma notificação para invocar a função Lambda.

<img width="893" height="236" alt="image" src="https://github.com/user-attachments/assets/3e1ee2fd-76fd-408f-b388-3ab1a2bff6fa" />

### Passos da Implementação

Criação do Bucket S3:

Um novo bucket S3 foi criado com um nome único. A configuração padrão foi mantida.

Criação da Função Lambda:

No console da AWS, uma nova função Lambda foi criada.

Runtime: Python 3.9 (ou outra versão de sua escolha).

Permissões: A função foi associada a uma política de execução que permite ler os objetos do bucket S3.

Configuração do Código da Função Lambda:

O código simples abaixo foi utilizado para demonstrar o processamento. Ele apenas exibe as informações do arquivo que acionou o evento, como o nome do bucket e a chave do objeto.

Python

import json

def lambda_handler(event, context):
    print("Evento recebido:", json.dumps(event))

    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        file_key = record['s3']['object']['key']
        file_size = record['s3']['object']['size']

        print(f"Novo arquivo '{file_key}' (tamanho: {file_size} bytes) foi adicionado no bucket '{bucket_name}'.")

    return {
        'statusCode': 200,
        'body': json.dumps('Processamento da função Lambda concluído com sucesso!')
    }

### Configuração do Gatilho S3:

No designer da função Lambda, adicionei o S3 como gatilho.

Selecionei o bucket S3 criado no passo 1.

Escolhi o tipo de evento "All object create events" para que a função fosse acionada sempre que um objeto fosse adicionado.

### Resultados e Aprendizados

Principais aprendizados foram:

Integração de Serviços: A facilidade de conectar o S3 e o Lambda para criar uma pipeline de processamento de dados.

Modelo de Computação Serverless: A capacidade de executar código sem gerenciar servidores, pagando apenas pelo tempo de execução.

Observabilidade: Utilizar os logs do CloudWatch para monitorar a execução da função Lambda e depurar problemas.

A prática de documentar cada passo no GitHub também reforçou a importância de manter um registro claro e organizado para projetos técnicos, facilitando a colaboração e a apresentação do trabalho.
