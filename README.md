# Android Crypto Monitor

API Android para monitoramento de cotações do Bitcoin usando a API do Mercado Bitcoin

## Estrutura do Projeto


### Modelos de Dados

  * TickerResponse.kt: Modelo da resposta da API

  * Ticker.kt: Modelo com dados do ticker (preços, volume, etc.)


### Serviço de API 

  *  MercadoBitcoinService.kt: Interface Retrofit para a API

  *  MercadoBitcoinServiceFactory.kt: Factory para criar instância do serviço

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

## Referências

  * https://square.github.io/retrofit/

  * https://github.com/google/gson

# Evidências


![Prova1](https://github.com/user-attachments/assets/62b9081a-1419-495d-aa98-fbfd03a551db)

![Prova2](https://github.com/user-attachments/assets/21b738fb-cafb-4d9d-b3eb-f468a982160c)
