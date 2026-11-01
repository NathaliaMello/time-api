# TIME API
## Descrição
Esta API retorna a data e hora atual em formato JSON.
Ela foi desenvolvida para suporte a aplicação Time App, também disponível neste repositório.
O motivo pelo qual optei por desenvolver essa API ao invés de utilizar uma API existente foi pela possibilidade de simular lentidão e falhas.
A api será disponibilizada "sem lentidão". Porém, é possível simular adicionando
```java
Thread.sleep(5000L);
```
no corpo do método `getTime()` e adicionando
```java
throws InterruptedException
```
na sua assinatura, uma vez que sleep lança uma exceção do tipo InterruptedException.

O Thread.sleep(5000L); faz com que a execução do método `getTime()` seja pausada por 5 segundos, simulando uma lentidão na resposta da API. Isso é útil para testar a resiliência da aplicação Time App em situações de lentidão ou falha na API.

Para que ambas aplicações rodem em paralelo na máquina local, está foi exposta na porta 8081. É possível mudar a porta através do application.properties.