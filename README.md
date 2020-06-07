# NewsApiCore
A port of the official News API client library to .NET Core (C#). 

All that has been done is to recompile to target .Net Core v3.1 and add this note. All other content is as was in the original repo: [https://github.com/News-API-gh/News-API-csharp](https://github.com/News-API-gh/News-API-csharp). 

No support is supplied but you're welcome to suggest improvements, pull requests and point out things that are wrong with this code. However, I don't work for NewsAPI so I can't fix their internals or have any advance notice of changes they might make.


# News API client library for .NET (C#)
News API is a simple HTTP REST API for searching and retrieving live articles from all over the web. It can help you answer questions like:

- What top stories is the NY Times running right now?
- What new articles were published about the next iPhone today?
- Has my company or product been mentioned or reviewed by any blogs recently?

You can search for articles with any combination of the following criteria:

- Keyword or phrase. Eg: find all articles containing the word 'Microsoft'.
- Date published. Eg: find all articles published yesterday.
- Source name. Eg: find all articles by 'TechCrunch'.
- Source domain name. Eg: find all articles published on nytimes.com.
- Language. Eg: find all articles written in English.

You can sort the results in the following orders:

- Date published
- Relevancy to search keyword
- Popularity of source

You need an API key to use the API - this is a unique key that identifies your requests. They're free for development, open-source, and non-commercial use. You can get one here: [https://newsapi.org](https://newsapi.org).

## Installation
The News API client library is available on Nuget. You can install it either through the Nuget package management window in Visual Studio by searching for NewsAPI, or by running the following in the package manager console:
```shell
PM> Install-Package NewsAPI
```

## Usage example
```csharp
using NewsAPI;
using NewsAPI.Models;
using NewsAPI.Constants;
using System;

namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            // init with your API key (get this from newsapi.org)
            var newsApiClient = new NewsApiClient("XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX");

            var articlesResponse = newsApiClient.GetEverything(new EverythingRequest
            {
                Q = "Apple",
                SortBy = SortBys.Popularity,
                Language = Languages.EN,
                From = new DateTime(2018, 1, 25)
            });

            if (articlesResponse.Status == Statuses.Ok)
            {
                // total results found
                Console.WriteLine(articlesResponse.TotalResults);

                // here's the first 20
                foreach (var article in articlesResponse.Articles)
                {
                    // title
                    Console.WriteLine(article.Title);
                    // author
                    Console.WriteLine(article.Author);
                    // description
                    Console.WriteLine(article.Description);
                    // url
                    Console.WriteLine(article.Url);
                    // image
                    Console.WriteLine(article.UrlToImage);
                    // published at
                    Console.WriteLine(article.PublishedAt);
                }
            }

            Console.ReadLine();
        }
    }
}
```
