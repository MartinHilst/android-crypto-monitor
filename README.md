# Android Crypto Monitor

API Android para monitoramento de cotações do Bitcoin usando a API do Mercado Bitcoin

## Estrutura do Projeto

### 1. TickerResponse

```
class TickerResponse(
    val ticker: Ticker
)
```
* Representa a resposta da API do Mercado Bitcoin.


```
class Ticker(
    val high: String,    // Maior preço recente  
    val low: String,     // Menor preço recente  
    val vol: String,     // Volume negociado  
    val last: String,    // Último preço negociado  
    val buy: String,     // Melhor preço de compra  
    val sell: String,    // Melhor preço de venda  
    val date: Long       // Timestamp da última atualização  
)
```
* Armazena os dados da cotação do Bitcoin.

### 2. MercadoBitcoinService

```
interface MercadoBitcoinService {
    @GET("api/BTC/ticker/")
    suspend fun getTicker(): Response<TickerResponse>
}
```
* Define o endpoint da API usando Retrofit.
  
  - @GET("api/BTC/ticker/") – Faz uma requisição GET para obter os dados do Bitcoin.

  - suspend fun getTicker() – Função suspensa (usada com corrotinas) que retorna um Response<TickerResponse>.

### 3. MercadoBitcoinServiceFactory
```
class MercadoBitcoinServiceFactory {
    fun create(): MercadoBitcoinService {
        val retrofit = Retrofit.Builder()
            .baseUrl("https://www.mercadobitcoin.net/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()

        return retrofit.create(MercadoBitcoinService::class.java)
    }
}
```
* Configura o Retrofit para fazer chamadas à API.

  - baseUrl("https://www.mercadobitcoin.net/") – Define a URL base da API.
  
  - addConverterFactory(GsonConverterFactory.create()) – Converte JSON em objetos Kotlin usando Gson.
  
  - retrofit.create(MercadoBitcoinService::class.java) – Cria uma instância do serviço.


### 4. MainActivity 
```
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)

    // Configura a Toolbar
    val toolbarMain: Toolbar = findViewById(R.id.toolbar_main)
    configureToolbar(toolbarMain)

    // Configura o botão Refresh
    val btnRefresh: Button = findViewById(R.id.btn_refresh)
    btnRefresh.setOnClickListener {
        makeRestCall()  // Faz a chamada à API quando clicado
    }
}
```
* Inicializa a interface e define o comportamento do botão.
  - makeRestCall() - Faz a chamada à API quando o botão é clicado

```
private fun makeRestCall() {
    CoroutineScope(Dispatchers.Main).launch {
        try {
            val service = MercadoBitcoinServiceFactory().create()
            val response = service.getTicker()

            if (response.isSuccessful) {
                val tickerResponse = response.body()
                updateUI(tickerResponse)  // Atualiza a UI com os novos dados
            } else {
                showError(response.code())  // Trata erros de resposta
            }
        } catch (e: Exception) {
            Toast.makeText(this@MainActivity, "Falha na chamada: ${e.message}", Toast.LENGTH_LONG).show()
        }
    }
}
```

* Faz a chamada à API e atualiza a interface.

  - Usa CoroutineScope(Dispatchers.Main) para executar em background e atualizar a UI na thread principal.

  - Verifica se a resposta foi bem-sucedida (response.isSuccessful).

  - Atualiza a UI ou exibe erros.

```
val lastValue = tickerResponse?.ticker?.last?.toDoubleOrNull()
if (lastValue != null) {
    val numberFormat = NumberFormat.getCurrencyInstance(Locale("pt", "BR"))
    lblValue.text = numberFormat.format(lastValue)
}

val date = tickerResponse?.ticker?.date?.let { Date(it * 1000L) }
val sdf = SimpleDateFormat("dd/MM/yyyy HH:mm:ss", Locale.getDefault())
lblDate.text = date?.let { sdf.format(it) }
```
* Exibe os dados formatados na interface.

  - Converte last para Double e formata como moeda brasileira.

  - Converte date para uma data legível.
  
## Dependências

  * Retrofit 2 - Requisições HTTP

  * Gson - Conversão JSON-Kotlin

## Referências

  * https://square.github.io/retrofit/

  * https://github.com/google/gson

# Evidências


![Prova1](https://github.com/user-attachments/assets/62b9081a-1419-495d-aa98-fbfd03a551db)

![Prova2](https://github.com/user-attachments/assets/21b738fb-cafb-4d9d-b3eb-f468a982160c)
