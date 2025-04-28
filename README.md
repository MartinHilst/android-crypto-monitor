# Android Crypto Monitor

API Android para monitoramento de cotações de criptomoedas usando a API do Mercado Bitcoin

## Estrutura do Projeto


### Modelos de Dados (model package)

  * TickerResponse.kt: Modelo da resposta da API

  * Ticker.kt: Modelo com dados do ticker (preços, volume, etc.)


### Serviço de API (service package)

  *  MercadoBitcoinService.kt: Interface Retrofit para a API

  *  MercadoBitcoinServiceFactory.kt: Fábrica para criar instância do serviço

## Funcionalidades

  * Obtém dados de ticker do Bitcoin da API do Mercado Bitcoin

  * Parseia resposta JSON para objetos Kotlin

  * Factory configurada para criar o serviço de API

## Configuração

  * URL base da API:

    - https://www.mercadobitcoin.net/  

## Como Usar

Para obter os dados do ticker:
  
```
val service = MercadoBitcoinServiceFactory().create()  
val response = service.getTicker()  
if (response.isSuccessful) {  
    val ticker = response.body()?.ticker  
    // Usar os dados (high, low, last, etc.)  
}  
```

## Dependências

  * Retrofit 2 - Requisições HTTP

  * Gson - Conversão JSON-Kotlin

Referências

  * https://square.github.io/retrofit/

  * https://github.com/google/gson
