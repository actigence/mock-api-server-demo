# Examples for Mock API Server

```$xslt
Mock API Server now supports XML response type. Simply add .xml files in the folder path to gett XML response. However, .json files will be given priority. If a folder path has both JSON and XML response files, JSON response will be used.
```

This repository contains examples on how to use [Mock API Server](http://mock-api-server.actigence.com) to generate dummy RESTful apis.

[Mock API Server](http://mock-api-server.actigence.com) is a simple way to create mock RESTful APIs. It allows you to define a JSON response for an API URL. It supports all the HTTP methods and you can also define different responses based on query params.

## Table of Content
1. [Creating Your First Mock API](#creating-your-first-mock-api)
2. [Using Path Variables In Mock APIs](#using-path-variables-in-mock-apis)
3. [Using Query Params in Mock APIs](#using-query-params-in-mock-apis)
4. [Examples In This Repo](#examples-in-this-repo)
5. [Postman Collection](#postman-collection)


### Creating Your First Mock API
[Mock API Server](http://mock-api-server.actigence.com) uses Github to fetch JSON response based on api URL. An api URL is mapped to the folders in the Github repository and a JSON file with name matching to HTTP method us returned.

1. Create a public Github repository. For example `mock-api-server-demo`.
2. Create a folder structure to mimic your api path. Eg. `/api/persons`.
3. Add separate JSON files for each HTTP method that you want to support at this api path. Example, for GET method add `get.json`, for POST method add `post.json` and so on. Make sure the file names are in lower case. 
4. That's it now you can access you dummy API using path https://dummyapi.actigence.com/api/{github-account}/{github-repo}/{github-branch}/api/persons.

### Using Path Variables In Mock APIs

[Mock API Server](http://mock-api-server.actigence.com) treats path variables as simple folders in your Github repository. 
Example, if you want to create an api with path `api/persons/100`, simply create a folder path `api/persons/100` in your repository and add the JSON response files there.

### Using Query Params in Mock APIs

[Mock API Server](http://mock-api-server.actigence.com) converts your query parameters to a repository folder, using following rules:
1. Sort the parameters.
2. Replaces all special characters with `-` (hyphen).
3. Merge all the parameters into a single folder name.

Example, an API path like `/api/persons/search?name=victor&country=CA` will result in folder structure as `/api/persons/search/country-US-name-victor`. 
You should create corresponding folder structure in your Github repository and add JSON files there.

If the folder structure with Query parameters is not found, Mock API Server will use URL path as backup folder structure. 
Example, with API path like `/api/persons/search?name=victor&country=CA` Mock API Server will first search for JSON file in folder `/api/persons/search/country-US-name-victor`. If no matching JSOON file is found, then it will search in folder `/api/persons/search`.

### Examples In This Repo

| Desired API Path                  | Http Method   | Repository Path                                                                                                                                   | Mock API Server URL                                                                                                       |
| --------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| /api/persons                      |    GET        | [/api/persons/get.json](https://github.com/actigence/mock-api-server-demo/blob/main/api/persons/get.json)                                         | [Click To Open](https://dummyapi.actigence.com/api/actigence/mock-api-server-demo/main/api/persons)                       |
| /api/persons                      |    POST       | [/api/persons/post.json](https://github.com/actigence/mock-api-server-demo/blob/main/api/persons/post.json)                                       | Use Postman Collection                                                                                                    |
| /api/persons/10000                |    GET        | [/api/persons/10000/get.json](https://github.com/actigence/mock-api-server-demo/blob/main/api/persons/10000/get.json)                             | [Click To Open](https://dummyapi.actigence.com/api/actigence/mock-api-server-demo/main/api/persons/10000)                 |
| /api/persons/search?name=victor   |    GET        | [/api/persons/search/name-victor/get.json](https://github.com/actigence/mock-api-server-demo/blob/main/api/persons/search/name-victor/get.json)   | [Click To Open](https://dummyapi.actigence.com/api/actigence/mock-api-server-demo/main/api/persons/search?name=victor)    |
| /api/persons/search?name=invalid  |    GET        | [/api/persons/search/get.json](https://github.com/actigence/mock-api-server-demo/tree/main/api/persons/search/get.json)                           | [Click To Open](https://dummyapi.actigence.com/api/actigence/mock-api-server-demo/main/api/persons/search?name=invalid)   |

### Postman Collection

This repository contains a Postman collection, that allows you to execute examples in this repository against 
[Mock API Server](http://mock-api-server.actigence.com).

To use the Postman collection, you will need to install [Postman API Client](https://www.postman.com/product/api-client/) 
and import both [example](https://github.com/actigence/mock-api-server-demo/blob/main/postman/mock-api-server-examples.json) 
and [environment](https://github.com/actigence/mock-api-server-demo/blob/main/postman/public_server.env.json) files. 
After that you will be able to execute the examples through your Postman installation.