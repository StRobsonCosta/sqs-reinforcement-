# Guia Rápido de AWS SQS

Este guia fornece comandos essenciais para gerenciar filas do Amazon Simple Queue Service (SQS) usando a AWS CLI, além de informações sobre configurações avançadas, como filas FIFO e Dead Letter Queues (DLQs).

## Configuração Inicial

Antes de usar os comandos abaixo, certifique-se de que:
- Você tem a AWS CLI instalada e configurada.
- Suas credenciais da AWS estão configuradas corretamente (`aws configure`).

## Criar uma Fila SQS

```sh
aws sqs create-queue --queue-name minha-fila
```

### Criar uma Fila FIFO

```sh
aws sqs create-queue --queue-name minha-fila.fifo --attributes FifoQueue=true
```

## Listar Filas Existentes

```sh
aws sqs list-queues
```

## Obter URL de uma Fila

```sh
aws sqs get-queue-url --queue-name minha-fila
```

## Obter Informações de uma Fila

```sh
aws sqs get-queue-attributes --queue-url <URL_DA_FILA> --attribute-names All
```

## Enviar Mensagem para uma Fila

```sh
aws sqs send-message --queue-url <URL_DA_FILA> --message-body "Minha mensagem"
```

### Enviar Mensagem para uma Fila FIFO

```sh
aws sqs send-message --queue-url <URL_DA_FILA_FIFO> --message-body "Minha mensagem" --message-group-id "meu-grupo"
```

## Receber Mensagens de uma Fila

```sh
aws sqs receive-message --queue-url <URL_DA_FILA>
```

## Excluir Mensagem de uma Fila

```sh
aws sqs delete-message --queue-url <URL_DA_FILA> --receipt-handle <RECEIPT_HANDLE>
```

## Criar e Vincular uma Dead Letter Queue (DLQ)

1. Criar a fila DLQ:

```sh
aws sqs create-queue --queue-name minha-dlq
```

2. Obter o ARN da DLQ:

```sh
aws sqs get-queue-attributes --queue-url <URL_DA_DLQ> --attribute-names QueueArn
```

3. Vincular a DLQ à fila principal:

```sh
aws sqs set-queue-attributes --queue-url <URL_DA_FILA> --attributes "RedrivePolicy={\"deadLetterTargetArn\":\"<ARN_DA_DLQ>\",\"maxReceiveCount\":\"5\"}"
```

## Excluir uma Fila

```sh
aws sqs delete-queue --queue-url <URL_DA_FILA>
```

## Configuração pelo Console AWS

### Criar uma Fila FIFO
1. Acesse o Console AWS e vá para SQS.
2. Clique em **Criar fila**.
3. Escolha **Fila FIFO**.
4. Defina um nome terminando em `.fifo`.
5. Configure atributos, como **Message Deduplication ID**.
6. Clique em **Criar fila**.

### Criar e Configurar uma DLQ
1. No Console AWS, crie uma nova fila (DLQ).
2. Copie o ARN da fila criada.
3. Acesse as configurações da fila principal.
4. Vá até **Dead-letter queue settings** e clique em **Edit**.
5. Escolha a DLQ e defina o **Max receive count**.
6. Salve as configurações.

Este guia cobre os principais comandos e configurações necessários para gerenciar filas no AWS SQS de maneira eficiente.

### Usando o Programa em Node:
1. No diretorio src do projeto abra o terminal (uso o VSCode mesmo)
2. npm init -y (caso ainda não tenha)
3. npm install aws-sdk (Precisa ter as credenciais da AWS)
4. execute o comando **node** para cada arquivo **js** que deseja rodar.
- ex.: 
5. node send-message.js 
6. node receive-messages.js 
