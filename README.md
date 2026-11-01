# Time API

## Descrição

A **Time API** é uma API simples que retorna a data e hora atual em formato JSON.

Ela foi desenvolvida para dar suporte à aplicação **Time App**, também disponível neste repositório, permitindo consultar o horário atual por meio de uma requisição HTTP.

Além do uso básico, esta API também pode ser utilizada para simular cenários de lentidão e falha, ajudando em testes de resiliência, timeout e comportamento da aplicação consumidora diante de instabilidades.

## Objetivo

O principal objetivo desta API é fornecer um endpoint simples para retorno da data e hora atual, permitindo que aplicações clientes possam consumir essa informação de forma rápida e previsível.

A decisão de desenvolver uma API própria, em vez de utilizar uma API pública existente, foi motivada pela necessidade de controlar o comportamento da resposta, especialmente para simular atrasos e testar a robustez da aplicação cliente.


```bash
 GET (http://localhost:8081/time-api) 
```
## Porta da aplicação
Por padrão, a aplicação está configurada para rodar na porta `8081`.

Essa configuração permite que a **Time API** e a aplicação **Time App** sejam executadas em paralelo na máquina local.

Caso necessário, a porta pode ser alterada no arquivo:
`application.properties`


## Executando a aplicação

Para iniciar a aplicação em modo de desenvolvimento, execute o comando abaixo na raiz do projeto:

````bash
mvn clean quarkus:dev
````
O comando `clean` é opcional, mas pode ser útil para garantir que o projeto seja recompilado do zero.

Também é possível executar apenas:
```bash
mvn quarkus:dev
```

## Testando a API

Após iniciar a aplicação, execute uma chamada HTTP para o endpoint:
```bash
curl http://localhost:8081/time-api
```

Para realizar chamadas repetidas em loop, utilize o comando abaixo no terminal:
```bash
while true do curl http://localhost:8081/time-api echo sleep 2 done
```

Esse comando executa uma requisição HTTP GET para `http://localhost:8081/time` a cada 2 segundos, exibindo o resultado no terminal.

Para interromper o loop sem fechar o terminal, pressione:

```bash
Ctrl + C
```


## Simulando lentidão na API

Por padrão, a API é disponibilizada sem atraso artificial na resposta.

Caso queira simular lentidão, adicione a instrução abaixo no corpo do método `getTime()`:

``java
Thread.sleep(5000);
``
Também será necessário adicionar a cláusula `throws InterruptedException` na assinatura do método:

Com essa alteração, a execução do método será pausada por 5 segundos antes de retornar a resposta.

Esse comportamento é útil para testar como a aplicação cliente lida com cenários como:

- lentidão na API;
- timeout;
- falhas temporárias;
- necessidade de retry;
- degradação controlada;
- resiliência da comunicação entre serviços.

## Tecnologias utilizadas

- Java
- Quarkus
- Maven

## Uso recomendado

Esta API pode ser utilizada como apoio em estudos e demonstrações sobre:
- consumo de APIs REST;
- comunicação entre aplicações;
- testes de resiliência;
- simulação de latência;
- tratamento de falhas em aplicações cliente.
