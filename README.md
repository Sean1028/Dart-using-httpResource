# Dart-using-httpResource
import "dart:convert";

// 引入套件
import "package:http/http.dart" as http;

void main() async{
  Uri url = Uri.parse('https://jsonplaceholder.typicode.com/users/1');
  var response = await http.get(url);
  
  //print (response.body);
  
  Map<String, dynamic> jsonObjectFromRemote = jsonDecode(response.body);
  //print(jsonObjectFromRemote['phone']);
  
   Uri multipleItemUrl = Uri.parse('https://jsonplaceholder.typicode.com/users');
   var multipleResponses = await http.get(multipleItemUrl);
   // 印出回應結果，確認回傳的 json 資料長相   
   //print(multipleResponses.body);
   // 轉換成 List
   List<dynamic> jsonArrayFromRemote = jsonDecode(multipleResponses.body);
   //print(jsonArrayFromRemote[0]);
  
    Uri postItemUrl = Uri.parse("https://jsonplaceholder.typicode.com/posts");
    // 使用 http 套件的 post 
    String postRequestJsonBody = jsonEncode({"userId": "99","title": '雲育鏈', "body": '半夜寫程式，累啊。'});
    var postResponse = await http.post(postItemUrl, body: postRequestJsonBody);
    print(postResponse.body);
    //這裡沒看得很懂為甚麼print出來會是id 101
  
}
