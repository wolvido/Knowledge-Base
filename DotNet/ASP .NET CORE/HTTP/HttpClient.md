---
keywords: |-
  how to connect to api 
  how to use api in a service 
  how to use third party api in a service
  How to consume api
---
The `HttpClient` class is used for sending HTTP requests and receiving HTTP responses. It is a versatile class that provides a simple and efficient way to interact with HTTP services.
It is what you use when you use third party API's.
# So how to implement?
#### First, when using MVC, then you should implement it in a service.
Going forward in this note, were going to assume were using this in a service.
>[!question]- If you dont know how
>  see this [[Services - Service layer]].

So, if your services is in the same project as your program, just add this in program.cs:
```c#
builder.Services.AddHttpClient();
```

If not, If it is in a separate class library, then you also have to install **`Microsoft.Extensions.Http`** (through nuget)  on that class library. 
>[!tip]
> best practice is to use a separate class library
#### IHttpClientFactory
IHttpClientFactory provides a method called CreateClient() that creates an instance of HttpClient, and automagically handles the disposing after usage. Without it you have to manually close it.
We need IHttpClientFactory because `IHttpClientFactory` is designed to address common issues related to managing the lifecycle of `HttpClient` instances, such as DNS changes, connection reuse, and avoiding resource exhaustion. It is considered best practice for managing instances of `HttpClient`.
So in your service, inject IHttpClientFactory:
```c#
public class CityWeatherApiService : ICityWeatherService
{
	private readonly IHttpClientFactory _httpClientFactory;
	
	public CityWeatherApiService(IHttpClientFactory httpClientFactory)
	{
		_httpClientFactory = httpClientFactory;
	}
	
	//The methods and codes here
}
```
#### IConfiguration
Ofcourse we need to store the api keys into the [[Secrets Manager]].

So we must inject IConfiguration in order to access the api keys:
```c#
public class CityWeatherApiService : ICityWeatherService
{
	private readonly IHttpClientFactory _httpClientFactory;
	
	private readonly IConfiguration _configuration;
	
	public CityWeatherApiService(IHttpClientFactory httpClientFactory, IConfiguration configuration)
	{
		_httpClientFactory = httpClientFactory;
		_configuration = configuration;
	}
	
	//The methods and codes here
}
```
>[!note]
>There might be a better way, instead of injecting the configuration, just let the controller give the api key to the service, that way the service does not depend on the configuration. But I'm not sure yet, will come back to this later. 
#### Create a model for the API Response
You need to create a model so the API response can be modeled in the model, and the data can be useful. see [[Model]].
for example in a weather app we create:
```c#
public class WeatherData
{
	[JsonPropertyName("coord")]
    public Coord Coord { get; set; }
    [JsonPropertyName("weather")]
    public List<Weather> Weather { get; set; }
    [JsonPropertyName("rain")]
    public Rain Rain { get; set; }
    [JsonPropertyName("clouds")]
    public Clouds Clouds { get; set; }
    [JsonPropertyName("id")]
    public int Id { get; set; }
    [JsonPropertyName("name")]
    public string Name { get; set; }
}

public class Coord
{
	[JsonPropertyName("lon")]
    public double Lon { get; set; }
    [JsonPropertyName("lat")]
    public double Lat { get; set; }
}

public class Weather
{
    [JsonPropertyName("id")]
    public int Id { get; set; }
    [JsonPropertyName("main")]
    public string Main { get; set; }
    [JsonPropertyName("description")]
    public string Description { get; set; }
    [JsonPropertyName("icon")]
    public string Icon { get; set; }
}

public class Rain
{
    [JsonPropertyName("1h")]
    public double Rain1h { get; set; }
}

public class Clouds
{
	[JsonPropertyName("all")]
    public int All { get; set; }
}
```
###### We created the model above because we expect the api to return an equivalent json:
```json
{
  "id": 3163858,
  "name": "TestCity",
  "coord": {
    "lon": 10.99,
    "lat": 44.34
  },
  , 
  "weather": [
	   { 
		   "id": 501, 
		   "main": "Rain", 
		   "description": 
		   "moderate rain", 
		   "icon": "10d" 
	   } 
   ],
  "rain": {
    "1h": 3.16
  },
  "clouds": {
    "all": 100
  }
}                        
```
>[!important]
>Notice we added the attribute 	`[JsonPropertyName("jsonEquivalentName")]` to every property, This is because we will use the json serializer later to model the json we receive. It will not know the equivalent property if the correct name is not set.
#### Send a Request to the API
After `IHttpClientFactory` and `IConfiguration` is set. We can send a request to the API.
Assuming this sample method is in a service.

sample method to send a request:
```c#
//sample method that makes requests to external api
//ofcourse it is an async method since were dealing with a third party
//WeatherData is the return type
public async Task<WeatherData> GetWeatherData(string city)
{
	//first create a using block
	//Inside the using parameter we create an instance of the client using the factory
	using (HttpClient client = _httpClientFactory.CreateClient())
	{
		//Then create the message to be sent to the request
		HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, $"https://api.openweathermap.org/data/2.5/weather?{city}&appid={_configuration["apiKey"]}");
		//HttpRequestMessage has two parameters, first is the http method(get, post, etc..)-
		//the second is the link of the api in string
		//were using _configuration["apiKey"] as the api-key since it is stored in secrets manager

		//Send the request and store the API response in response type HttpResponseMessage
		HttpResponseMessage response = await client.SendAsync(request);
		
		//ofcourse the respons will be an http response, and is unreadable
		//so first convert it to string, the response will return a Json
		string responseContent = await response.Content.ReadAsStringAsync();
		
		//After that, Response content is still in Json so we need to model it to a model
		//so that it can be usefull
		WeatherData? weatherData = JsonSerializer.Deserialize<WeatherData>(responseContent);
		
		if (cityWeather == null) //also validation of course
		{
		    throw new InvalidOperationException("CityWeather is null");
		}
		
		return weatherData;
	}
}
```
**`weatherData`** will now be an initialized concrete model with data from the api, to use it as needed.
Assuming you know how services and controllers work, then you can use this service as needed.
see: [[Services - Service layer]] on how services is used.

>[!note]
>take note there might be other api's that do not return a content that can be converted to string, if thats the case you can use .ReadAsStreamAsync(); then read the stream using appropriate methods