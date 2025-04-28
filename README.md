# Android Crypto Monitor

API Android para monitoramento de cotações do Bitcoin usando a API do Mercado Bitcoin

## Estrutura do Projeto

### 1. TickerResponse e Ticker

   * TickerResponse: Classe que representa a resposta da API, contendo um objeto Ticker

   * Ticker: Classe que armazena os dados da cotação, incluindo:

       - Valores (high, low, last, buy, sell)

       - Volume de negociação (vol)

       - Momento da cotação (date)

### 2. MercadoBitcoinServiceFactory

Responsável por criar uma instância do serviço Retrofit configurada para:

   * Usar a URL base do Mercado Bitcoin

   * Converter respostas JSON para objetos Kotlin usando Gson

### 3. MercadoBitcoinService

* Interface que define os endpoints da API:

    - getTicker(): Requisição GET para obter os dados de ticker do Bitcoin

### 4. MainActivity 

Responsável pela UI e interação com o usuário:

   * Configura a Toolbar

   * Implementa o botão de refresh

   * Faz chamadas à API usando corrotinas

   * Atualiza a UI com os dados recebidos

   * Formata valores e datas para exibição

   * Trata erros e exibe mensagens

## Dependências

  * Retrofit 2 - Requisições HTTP

  * Gson - Conversão JSON-Kotlin

## Referências

  * https://square.github.io/retrofit/

  * https://github.com/google/gson

# Evidências


![Prova1](https://github.com/user-attachments/assets/62b9081a-1419-495d-aa98-fbfd03a551db)

![Prova2](https://github.com/user-attachments/assets/21b738fb-cafb-4d9d-b3eb-f468a982160c)
