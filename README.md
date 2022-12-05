# ApiRest with RestSharp and Newtonsoft

```c#
var client = new RestClient("http://localhost:8069/api/create_fingerprint/13310091Z/1/x1234567890");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Content-Type", "text/plain");
request.AddHeader("Cookie", "session_id=dc0634779f7322409f148acaa5aa1e29fbc7d8b0");
var body = @"{" + "\n" +
@"    ""fingerprint"" : ""skjajsasnkanskjaskjnjkjkkj""" + "\n" +
@"}";
request.AddParameter("text/plain", body,  ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```c#
using System.Net;
using RestSharp;
using Newtonsoft.Json;

// "Project" -> "Manage NuGet packages" -> "Search for "newtonsoft json". -> click "install".
// "Project" -> "Manage NuGet packages" -> "Search for "RestSharp". -> click "install".


var _vat = "00102815511";

var _token = "x1234567890";
var path = "get_fingerprint";

path = "create_fingerprint";

if (path == "get_fingerprint")
  {

    Console.WriteLine("get_fingerprint");
    var _id = 6;
    Uri baseUrl = new Uri("http://master.odooerp.online/api/get_fingerprint/" + _vat + "/" + _id + "/" + _token);
    var client = new RestClient(baseUrl);
    var request = new RestRequest();
    var response = await client.GetAsync(request);


    if (response.StatusCode == HttpStatusCode.OK)
    {
        string rawResponse = response.Content;
        dynamic obj = JsonConvert.DeserializeObject(rawResponse);
        var huella = obj.fingerprint;
        // Console.WriteLine(obj);
        Console.WriteLine(huella);
    }

 }
else
 {
    Console.WriteLine("create_fingerprint");
    var _huella = "NuevaHuella";
    var _id = 7;
    Uri baseUrl = new Uri("http://master.odooerp.online/api/create_fingerprint/" + _vat + "/" + _id + "/" + _huella + "/"  + _token);
    var client = new RestClient(baseUrl);
    var request = new RestRequest();
    var response = await client.PostAsync(request);

    if (response.StatusCode == HttpStatusCode.OK)
    {
        string rawResponse = response.Content;
        dynamic obj = JsonConvert.DeserializeObject(rawResponse);
        var code = obj.code;
        // Console.WriteLine(obj);
        Console.WriteLine(code);
        if (code == "1")
        {
            Console.WriteLine("Se creo");
        } else
        {
            Console.WriteLine("No se creo");
        }
    }
}



Console.ReadLine();
```
