## Core Components
1. URLSession 
3. Codable Protocol
5. Result Type

## Networking Playgrounds

Using Swift Playgrounds is a good way to test network calls without having to implement them inside of an app.

## Codable 

Codable is a combination of the old decoupled Decodable/Encodable protocols from early swift. Codable will allow an object to transform itself into and out of JSON representation. You can encode and decode JSON in swift using the `JSONEncoder()` and `JSONDecoder()` methods.

## Coding Keys

If the keys coming from the JSON data aren't exactly what you want, you can use the CodingKeys enum to set your own property names. For example, if the JSON coming in is using snake casing, CodingKeys will allow you to convert the snake case into camel casing.

## URLSession

URLSession's dataTask method is what's most commonly used to fetch data from the net. The dataTask will return an optional data, response, and error in the completion block to use for decoding and error handling.

## Result 

The result type allows you to easily return back success/failure networking requests. You can use a switch statement on the result type to handle the success and failure cases. 

## Notes

[Examples of JSON conversion](https://github.com/jrasmusson/level-up-swift/blob/master/11-JSON/1-json.md)  
[HTTP in Swift](https://davedelong.com/blog/2020/06/27/http-in-swift-part-1/)
