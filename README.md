# Google Shopping Light API

SerpApi的Google Shopping Light API可以让你极高速度抓取Google Shopping的结果。Google Shopping Light引擎仅保留最核心的数据，不包含常规Google Shopping页面中能获取的额外信息，相比标准的[Google Shopping API](https://serpapi.com/google-shopping-api)它能够提供更快的响应速度。

该 API 可通过以下端点进行访问：/search?engine=google_shopping。

你可以通过发送 GET 请求查询：https://serpapi.com/search?engine=google_shopping&q=coffee 或者您可以前往[Playground](https://serpapi.com/playground?engine=google_shopping)体验实时、可交互的官方演示。

## API 调用参数

1. **查询关键字**

| 参数名 | 必填 | 描述                                                      |
|-----|----|---------------------------------------------------------|
| q   | 必填 | 本参数定义搜索的关键字<br>你可以定义任何你希望在Google Shopping search中搜索的内容。 |

2. **地理位置**

| 参数名      | 必填 | 描述                                                                                                                                                                                                                                                        |
|----------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| location | 可选 | 本参数定义你希望搜索发起的地理位置<br>如果有多个地理位置符合请求，我们会选取最多请求数的地理位置。<br><br>在[/locations.json API](https://serpapi.com/locations-api)查看更多关于控制精准地理位置请求的信息。<br>⚠️"location"参数与"uule"参数不能同时使用<br>建议使用"location"参数将位置信息指定到城市级别以模拟真实用户请求。如果"location"参数未指定位置，搜索将可能使用代理服务器所在的位置。 |
| uule     | 可选 | 本参数是Google加密的位置信息，"uule"与"location"参数不能同时使用。                                                                                                                                                                                                              |

3. **本地化**

| 参数名           | 必填 | 描述                                                                                                                                                          |
|---------------|----|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| google_domain | 可选 | 本参数定义Google使用的域名，默认为 google.com，<br>查看[Google domains](https://serpapi.com/google-domains)获取受支持的Google域名完整列表。                                               |
| gl            | 可选 | 本参数定义Google搜索使用的国家。<br>这个参数是一个两个字符的国家代码(例如：美国为us，英国为uk，法国为fr)。<br>查看[Google Shopping countries](https://serpapi.com/google-shopping-countries)获取受支持的国家完整列表。 |
| hl            | 可选 | 本参数定义Google搜索的语言，<br>这个参数是一个两个参数的语言代码(例如：英语为en，简体中文为zh-cn，zh-tw为繁体中文)，<br>查看[Google languages](https://serpapi.com/google-languages)获取受支持的语言完整列表。           |

4. **高级过滤器**

| 参数名            | 必填 | 描述                                                                                                                                                                                                                                                                                                                                                                            |
|----------------|----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| shoprs         | 可选 | 本参数定义一个包含查询及搜索过滤器相关metadata的token。<br>⚠️"q"参数与"shoprs"并不是必须同时使用。<br>如果要应用多个过滤器，可以使用&#124;&#124;连接，比如 shoprs_1&#124;&#124;shoprs_2&#124;&#124;shoprs_3。<br>该参数的可用值无法通过 Google Shopping Light API 获取。<br>你可以使用我们的 [Google Shopping API](https://serpapi.com/google-shopping-api) 来获取这些值，<br>或者直接访问 Google Shopping 网站，设置你需要的过滤条件，<br>然后将其 URL 中的 shoprs 值复制到 SerpApi 的 URL 中即可。 |
| min_price      | 可选 | 本参数定义最低价格。<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                                                                                  |
| max_price      | 可选 | 本参数定义最高价格。<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                                                                                  |
| sort_by        | 可选 | 本参数定义排序方式。<br><br>可用选项:<br>1 - Price:low to high<br>2 - Price:high to low<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                       |
| free_shipping  | 可选 | 只显示包邮产品。<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                                                                                    |
| on_sale        | 可选 | 只显示折扣产品。<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                                                                                    |
| small_business | 可选 | 只显示零售商。<br><br>(⚠️本参数会覆盖"shoprs"参数中所包含的对应过滤器)                                                                                                                                                                                                                                                                                                                                     |

5. **页码**

| 参数名    | 必填  | 描述                                                                                                |
|--------|-----|---------------------------------------------------------------------------------------------------|
| start  | 可选  | 参数定义返回结果开始的坐标，<br>设置这个参数可以跳过设置值数量的结果<br>(比如 默认值为0，则返回结果从第一页开始，10 是返回结果第二页开始，20 是返回结果从第三页开始，以此类推)。 |

## API 返回示例
- GET 方法
```text
https://serpapi.com/search.json?engine=google_shopping_light&q=macbook
```

- java 代码
```text
Map<String, String> parameter = new HashMap<>();

parameter.put("engine", "google_shopping_light");
parameter.put("q", "macbook");
parameter.put("api_key", "secret_api_key");

GoogleSearch search = new GoogleSearch(parameter);

try {
  JsonObject results = search.getJson();
} catch (SerpApiSearchException ex) {
  System.out.println("Exception:");
  System.out.println(ex.toString());
}
```

- 返回示例
```text
{
  "search_metadata": {
    "id": "68ac3120ac297806b578ab76",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/5a11fa61c9ab5580/68ac3120ac297806b578ab76.json",
    "created_at": "2025-08-25 09:47:12 UTC",
    "processed_at": "2025-08-25 09:47:12 UTC",
    "google_shopping_light_url": "https://www.google.com/search?udm=28&q=macbook&hl=en&gl=us",
    "raw_html_file": "https://serpapi.com/searches/5a11fa61c9ab5580/68ac3120ac297806b578ab76.html",
    "total_time_taken": 1.16
  },
  "search_parameters": {
    "engine": "google_shopping_light",
    "q": "macbook",
    "google_domain": "google.com",
    "hl": "en",
    "gl": "us",
    "device": "desktop"
  },
  "search_information": {
    "shopping_results_state": "Results for exact spelling"
  },
  "shopping_results": [
    {
      "position": 1,
      "title": "2024 Apple MacBook Air 13.6\" M3 GPU 4.0GHz RAM 256GB SSD",
      "product_link": "https://www.google.com/shopping/product/2022324658094041775?gl=us",
      "product_id": "2022324658094041775",
      "immersive_product_page_token": "eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiMjAyMjMyNDY1ODA5NDA0MTc3NSIsImhlYWRsaW5lT2ZmZXJEb2NpZCI6IjExNDYyMDIzNzc1ODM4NTU1NDc0IiwiaW1hZ2VEb2NpZCI6IjQ3NTkzMDI4OTMwNjEzODYxODkiLCJyZHMiOiJQQ18zMzc2NDcxMzkwMTMyMTkyNDU2fFBST0RfUENfMzM3NjQ3MTM5MDEzMjE5MjQ1NiIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiMzM3NjQ3MTM5MDEzMjE5MjQ1NiIsIm1pZCI6IjU3NjQ2Mjc5MDk4MjgyNTQ5MiIsInB2dCI6ImhnIiwidXVsZSI6bnVsbCwiZ2wiOiJ1cyIsImhsIjoiZW4iLCJlbmdpbmUiOiJnb29nbGVfc2hvcHBpbmdfbGlnaHQifQ==",
      "serpapi_immersive_product_api": "https://serpapi.com/search.json?engine=google_immersive_product&page_token=eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiMjAyMjMyNDY1ODA5NDA0MTc3NSIsImhlYWRsaW5lT2ZmZXJEb2NpZCI6IjExNDYyMDIzNzc1ODM4NTU1NDc0IiwiaW1hZ2VEb2NpZCI6IjQ3NTkzMDI4OTMwNjEzODYxODkiLCJyZHMiOiJQQ18zMzc2NDcxMzkwMTMyMTkyNDU2fFBST0RfUENfMzM3NjQ3MTM5MDEzMjE5MjQ1NiIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiMzM3NjQ3MTM5MDEzMjE5MjQ1NiIsIm1pZCI6IjU3NjQ2Mjc5MDk4MjgyNTQ5MiIsInB2dCI6ImhnIiwidXVsZSI6bnVsbCwiZ2wiOiJ1cyIsImhsIjoiZW4iLCJlbmdpbmUiOiJnb29nbGVfc2hvcHBpbmdfbGlnaHQifQ%3D%3D",
      "source": "Microless.com",
      "source_icon": "https://encrypted-tbn3.gstatic.com/favicon-tbn?q=tbn%3AANd9GcQqzxzE9Tyq8gHIRWCVfZZfCqHk9cUK739sw4HpBF2TYkDknNLEiw0ZYAcvIpv5-I6igg95Y0okKUuMnTSlgV0mhJcqOBfv",
      "multiple_sources": true,
      "price": "$1,123.01",
      "extracted_price": 1123.01,
      "rating": 4.8,
      "reviews": 5600,
      "thumbnail": "https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcTeLClMwlJlENYNeS3WzBl14ykzaf5omK4c0dDwuFhlvfiobMhfCqQJsE6isvHij0XrgPW_R_qwAoce61XdcKPMdd2bb-6hifuddYND1xGZGwQSTA-pmK1B",
      "serpapi_thumbnail": "https://serpapi.com/images/url/jY-ElXicDclJDoIwAADAF7FUkUQSY9jEgBBcEpcLgbbQaqHFVlAf5X_8jc51vh-ilJCOYeAO3l9CYaSpqgN6I1WpKNQhbw1JuBC0a5b94n-Om6F5BA9447N0ZDELs3OG99Pj22PAet3eZT3jbWJBEwXjY0XYUFNepaT2-20sQ5vKYU2v5une5MdiV_SjyyG2wQnBJE8RmlSVZhNaPxA6ZwF4Rpdo3O4PribaBHg_iPk_CA"
    },
    {
      "position": 2,
      "title": "\"Apple MacBook Pro M1 Pro Restored",
      "product_link": "https://www.google.com/shopping/product/597336626086660347?gl=us",
      "product_id": "597336626086660347",
      "immersive_product_page_token": "eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiNTk3MzM2NjI2MDg2NjYwMzQ3IiwiaGVhZGxpbmVPZmZlckRvY2lkIjoiMTE3MDg2MjgyOTIxMjAyODY0MjgiLCJpbWFnZURvY2lkIjoiMTIxNzczMjI2NTU3NDAyMTAxNjgiLCJyZHMiOiJQQ182NDk5MDk0Mjc3MTE1MDMzODExfFBST0RfUENfNjQ5OTA5NDI3NzExNTAzMzgxMSIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiNjQ5OTA5NDI3NzExNTAzMzgxMSIsIm1pZCI6IjU3NjQ2Mjc4OTQ1NDkxODMyOSIsInB2dCI6ImhnIiwidXVsZSI6bnVsbCwiZ2wiOiJ1cyIsImhsIjoiZW4iLCJlbmdpbmUiOiJnb29nbGVfc2hvcHBpbmdfbGlnaHQifQ==",
      "serpapi_immersive_product_api": "https://serpapi.com/search.json?engine=google_immersive_product&page_token=eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiNTk3MzM2NjI2MDg2NjYwMzQ3IiwiaGVhZGxpbmVPZmZlckRvY2lkIjoiMTE3MDg2MjgyOTIxMjAyODY0MjgiLCJpbWFnZURvY2lkIjoiMTIxNzczMjI2NTU3NDAyMTAxNjgiLCJyZHMiOiJQQ182NDk5MDk0Mjc3MTE1MDMzODExfFBST0RfUENfNjQ5OTA5NDI3NzExNTAzMzgxMSIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiNjQ5OTA5NDI3NzExNTAzMzgxMSIsIm1pZCI6IjU3NjQ2Mjc4OTQ1NDkxODMyOSIsInB2dCI6ImhnIiwidXVsZSI6bnVsbCwiZ2wiOiJ1cyIsImhsIjoiZW4iLCJlbmdpbmUiOiJnb29nbGVfc2hvcHBpbmdfbGlnaHQifQ%3D%3D",
      "source": "GainSaver",
      "source_icon": "https://encrypted-tbn2.gstatic.com/favicon-tbn?q=tbn%3AANd9GcT7SHF6HqUHcCAVRhUBhi0Dcg-zeRkAkaF_Oh2cbMDyW5JSWp5ehhonOU4vyBvS6mzoxiWk0jxrQsGHZuGt8Ll8YQjXC7dB3L4t",
      "multiple_sources": true,
      "price": "$1,253.00",
      "extracted_price": 1253,
      "rating": 4.7,
      "reviews": 2300,
      "thumbnail": "https://encrypted-tbn0.gstatic.com/shopping?q=tbn:ANd9GcQxgKfI-6rPyjrkwoGQsagjI4V-sADhpg9be6wwYg8ZcRSw7OzYN79lRmLUhJocln6JgOR4fjIOerg0h0QPDaTON59qrwMP",
      "serpapi_thumbnail": "https://serpapi.com/images/url/oh7ihnicDcndCoIwGADQJ_LnwrQJEYIgWjm1H6g7nfObpnNug2UP0rv1NnVuz_fDtBYqdBzKiVyFpq2lG-7aoHSte2KTeXIUm4XoOeyX3f_CKG9RQsoXHLrU8mWxDvJp5qRUNQypd7NUFDMBqKG-MXfYPkh1NgF-3_MAjdV0vLJsJiP3M8CV1w0pphJc5pZFXF9wvkGLNKfiB97yNnE",
      "delivery": "Free delivery"
    },
    {
      "position": 3,
      "title": "Apple MacBook Pro 16 M4",
      "product_link": "https://www.google.com/shopping/product/5391602780257398368?gl=us",
      "product_id": "5391602780257398368",
      "immersive_product_page_token": "eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiNTM5MTYwMjc4MDI1NzM5ODM2OCIsImhlYWRsaW5lT2ZmZXJEb2NpZCI6IjE2MzU3NDA5ODczNzMyMTQ0MzQyIiwiaW1hZ2VEb2NpZCI6IjE0NTM0ODgwNjQ2MDQzNjY2NjQxIiwicmRzIjoiUENfNTAzMTc3MTMzNzU0Nzc4ODYyOHxQUk9EX1BDXzUwMzE3NzEzMzc1NDc3ODg2MjgiLCJxdWVyeSI6Im1hY2Jvb2siLCJncGNpZCI6IjUwMzE3NzEzMzc1NDc3ODg2MjgiLCJtaWQiOiI1NzY0NjI4MTYwNjMzNjIwOTIiLCJwdnQiOiJoZyIsInV1bGUiOm51bGwsImdsIjoidXMiLCJobCI6ImVuIiwiZW5naW5lIjoiZ29vZ2xlX3Nob3BwaW5nX2xpZ2h0In0=",
      "serpapi_immersive_product_api": "https://serpapi.com/search.json?engine=google_immersive_product&page_token=eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiNTM5MTYwMjc4MDI1NzM5ODM2OCIsImhlYWRsaW5lT2ZmZXJEb2NpZCI6IjE2MzU3NDA5ODczNzMyMTQ0MzQyIiwiaW1hZ2VEb2NpZCI6IjE0NTM0ODgwNjQ2MDQzNjY2NjQxIiwicmRzIjoiUENfNTAzMTc3MTMzNzU0Nzc4ODYyOHxQUk9EX1BDXzUwMzE3NzEzMzc1NDc3ODg2MjgiLCJxdWVyeSI6Im1hY2Jvb2siLCJncGNpZCI6IjUwMzE3NzEzMzc1NDc3ODg2MjgiLCJtaWQiOiI1NzY0NjI4MTYwNjMzNjIwOTIiLCJwdnQiOiJoZyIsInV1bGUiOm51bGwsImdsIjoidXMiLCJobCI6ImVuIiwiZW5naW5lIjoiZ29vZ2xlX3Nob3BwaW5nX2xpZ2h0In0%3D",
      "source": "Best Buy",
      "source_icon": "https://encrypted-tbn0.gstatic.com/favicon-tbn?q=tbn%3AANd9GcRJLrYt8ApvztGsW8TSy6-5HL7LwDNwH2emYmRabMUepMDXWE3LqD_Jltucg6NfE5z5MV57q9G1n_VVMyiUtZCVGXOuFlVA6g",
      "multiple_sources": true,
      "price": "$2,249.00",
      "extracted_price": 2249,
      "old_price": "$2,499",
      "extracted_old_price": 2499,
      "rating": 4.8,
      "reviews": 1500,
      "thumbnail": "https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcQkj91HOJRqa0O_jzw-zi6pQrlg1g8tnGNiFlAhwoj398a1DdiFa8yljnhI_AlptequunoEVAJVAcdcav6xiykBWCqY0HI7aNlVd0ijPhwTyRM7-fJrXq_-",
      "serpapi_thumbnail": "https://serpapi.com/images/url/Htwq_nicDc1JDoIwAADAF1UgJiwmxtQNJRGFGNQTqS3S1toFqgiP8j_-Rs9zmO-HWqvbieNUEje9thUB9iq9Ud1aZBkeYfVwWqq0ZrKemenfJjAlUYyzO4-8zT7JDXL3JR86MDBfZ42ovTq0Mk7ZWkDaKT6OQuQtCVujsBdc0m0Jxf8xz6dUqwImBcQEo5f_Zv19flqYi7vZBigVBXEZP9Du2Oe7ANyS5mxK8AN6jD9g",
      "tag": "10% OFF",
      "extensions": [
        "10% OFF"
      ],
      "delivery": "Free delivery"
    },
    ...
  ],
  "inline_shopping_results": [
    {
      "position": 1,
      "block_position": "top",
      "title": "Apple MacBook Air 13.3 inch Laptop - Space Gray, M1 Chip, Built for Apple Intelligence, 8GB Ram, 256gb storage",
      "price": "$599.00",
      "extracted_price": 599,
      "old_price": "$649",
      "extracted_old_price": 649,
      "link": "https://www.walmart.com/ip/Apple-MacBook-Air-13-3-inch-Laptop-Space-Gray-M1-Chip-8GB-RAM-256GB-storage/609040889?wmlspartner=wlpa&selectedSellerId=0",
      "tracking_link": "https://www.google.com/aclk?sa=L&ai=DChcSEwiE_rOF16WPAxVHRP8BHWHUH-gYABABGgJtZA&co=1&ase=2&gclid=EAIaIQobChMIhP6zhdeljwMVR0T_AR1h1B_oEAQYASABEgJq5_D_BwE&cce=2&category=acrcp_v1_32&sig=AOD64_0pntp7_teHQnF7WFzIUt4eNtmImQ&ctype=5&q=&nis=4&ved=2ahUKEwilxq-F16WPAxVvCnkGHbwwOPoQ5bgDKAB6BAgCEAs&adurl=",
      "source": "Walmart",
      "rating": 4.7,
      "reviews": 9000,
      "thumbnail": "https://encrypted-tbn0.gstatic.com/shopping?q=tbn:ANd9GcRb4HuuWc0l83icbZJp3VbU4B9Vr5j6SzuQDIiBF4rXCq8XDbuidvtj2w7IvdZ7BNBApoq7qWntxCdoU4OkQxGmSJGS-w3D1xGn6K85QvfD4UeVKzgaCAyGXcJEMuo845ie6R8yVOmlEYc&usqp=CAc",
      "serpapi_thumbnail": "https://serpapi.com/images/url/d5-UQXicDclLcoIwAADQ27hTVAJEZ5wOH5uKow4yILozCWKs5AMJgofsvrdp3_b9_ty1lu3SskpOmkHqko415tNJ1eqrZmRCRG21dyEl49WHWv3f0t_TBSJHDL6MOZHpE9qM4Ess7RxnIFjkjfNw07dJog0LPkFThAoWETaMdvoxf3mbjl68YB_4UihPnbjuQyoycPhOelSnMUrHLzua9Yi7W-gk3S0CWZlv39U19AdUkHi9MwICh5XuEQ75oX6uz2RkWiVXoU_-AJDRSHs",
      "extensions": [
        "256 GB drive",
        "8 GB Supported",
        "Space Gray",
        "8 GB RAM",
        "MacBook Air",
        "2560 x 1600",
        "Mac OS",
        "Octa Core",
        "USB-C",
        "Solid State Drive",
        "Sale"
      ],
      "tag": "Sale"
    },
    {
      "position": 2,
      "block_position": "top",
      "title": "Apple - MacBook Air 13-inch Laptop - Apple M4 chip Built for Apple Intelligence - 16GB Memory - 256GB SSD - Midnight",
      "price": "$799.00",
      "extracted_price": 799,
      "old_price": "$999",
      "extracted_old_price": 999,
      "link": "https://www.bestbuy.com/product/apple-macbook-air-13-inch-laptop-apple-m4-chip-built-for-apple-intelligence-16gb-memory-256gb-ssd-midnight/JJGCQ8RH7G/sku/6565862?ref=212&loc=1&utm_source=feed&extStoreId=834",
      "tracking_link": "https://www.google.com/aclk?sa=L&ai=DChcSEwiE_rOF16WPAxVHRP8BHWHUH-gYABADGgJtZA&ae=2&co=1&ase=2&gclid=EAIaIQobChMIhP6zhdeljwMVR0T_AR1h1B_oEAQYAiABEgKIEfD_BwE&cce=2&category=acrcp_v1_71&sig=AOD64_1fONbmdBV_U2RDD2fWTNWo-mD45Q&ctype=46&q=&ved=2ahUKEwilxq-F16WPAxVvCnkGHbwwOPoQ5bgDKAB6BAgCEB0&adurl=",
      "source": "Best Buy",
      "rating": 4.9,
      "reviews": 4000,
      "thumbnail": "https://encrypted-tbn2.gstatic.com/shopping?q=tbn:ANd9GcR6ZZpBL0Vm04_W13NFFIc5MIDwlnyXI7X1akDutYx7Jc1ObxlfFiRbCDve6rU3owkVbrJgDyShOYYwVhWR1sv7zGdl6luIa4sxqRT_vS4SyDs_BXFcNHuj5V2znLSe-icrN7_J3qYtgpA&usqp=CAc",
      "serpapi_thumbnail": "https://serpapi.com/images/url/UKmpdHicDcnfDkJQHADgt-muJGLZrKkzxaSNEt0YP0JxHM7xr4fsvrep7_b7fnLGCFU4LsXQToSlyZzFeLXIKItYAQuoK47mNSEFzraN-j9Fs5PNARzpfic7a-lVSzG88YKt6wasTwYaSjz5huzz0Qt1LBhlE_hzPJYPvXDiPepTqb0K9fDy4tbM0OTm5yAYvPzm8LSX34eklMrOiEQ6Ns4l7F3RnRANd74O9rF7rr3VG1tuOi-gteXQFJqAZUSbdbQh6l6DH6o6SbA",
      "extensions": [
        "Pick up today",
        "256 GB drive",
        "Midnight",
        "16 GB RAM",
        "MacBook Air",
        "2560 x 1664",
        "Mac OS",
        "Octa Core",
        "USB-C, HDMI, 3.5 mm Jack",
        "Sale"
      ],
      "tag": "Sale"
    },
    {
      "position": 3,
      "block_position": "top",
      "title": "Apple 16 MacBook Pro Retina Touch Bar (2019) 2.6GHz 6Core i7, Space Gray Used, by Apple",
      "price": "$449.00",
      "extracted_price": 449,
      "link": "https://eshop.macsales.com/configure-my-mac/apple-macbook-pro-retina-touch-bar-16-inch-late-2019?sku=UARA1JS412XXXXC&utm_source=google&utm_medium=shoppingengine&utm_campaign=googlebase",
      "tracking_link": "https://www.google.com/aclk?sa=L&ai=DChcSEwiE_rOF16WPAxVHRP8BHWHUH-gYABAFGgJtZA&co=1&ase=2&gclid=EAIaIQobChMIhP6zhdeljwMVR0T_AR1h1B_oEAQYAyABEgLjKfD_BwE&cce=2&category=acrcp_v1_32&sig=AOD64_2xy8Jof-Y7uUmfhEmQ7sywIgg-1A&ctype=5&q=&nis=4&ved=2ahUKEwilxq-F16WPAxVvCnkGHbwwOPoQ5bgDKAB6BAgCEDM&adurl=",
      "source": "OWC",
      "rating": 4.5,
      "reviews": 3000,
      "thumbnail": "https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcTSJZoJeecq-rwMpUXswYLIj_P6tbh-AlL5p0_z4sULj0Wxsh00EgrK50X20WAxKFkyCvgKG3-uvT0wv3FEXukoap4sgb2Y0nlwfPl1QPoQdrM2oSr12zUrqWJsLtMAMZvAK_8Sy-5mYg&usqp=CAc",
      "serpapi_thumbnail": "https://serpapi.com/images/url/L72UU3icDcndCoIwGADQt-luOTWjgogRFfkThonajeS0WZmb-6Zm79gD9DZ1bs_3UyolYKFpRU3lIFSRI5XV-piBuqgbHVP-1KDkQtxqtmqW_1uQQz7f0VNgn7ldFLRBsvdEGEOfuPt76k9VViJSuZbA6XsCoXvH0QtKjDdMOhaODRyRl7N9DOuOOTsTtd0J95253cTtg1_EBFhmJLiu-qtf6UefH3PpGTyQuvEOZRPZ4CqPeOeOOOksGJD1TNiohUYs14T-AJvHSRo",
      "extensions": [
        "512 GB drive",
        "Space Gray",
        "16 GB RAM",
        "MacBook Pro",
        "Mac OS",
        "Hexa Core",
        "USB-C, 3.5 mm Jack",
        "Solid State Drive",
        "16 inches"
      ]
    },
    ...
  ],
  "categorized_shopping_results": [
    {
      "title": "MacBook Air",
      "description": "Lightweight and portable, with impressive performance and long battery life. Ideal for everyday tasks.",
      "shopping_results": [
        {
          "position": 1,
          "title": "Apple 13-inch MacBook Air M4 10-core CPU",
          "product_link": "https://www.google.com/shopping/product/16918290957317259408?gl=us",
          "product_id": "16918290957317259408",
          "immersive_product_page_token": "eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiMTY5MTgyOTA5NTczMTcyNTk0MDgiLCJoZWFkbGluZU9mZmVyRG9jaWQiOiI5MjU4MjYyMDQ3MzkzNzgxMDMxIiwiaW1hZ2VEb2NpZCI6IjEzNjQ1MDYwMTEzNzY0NzI4MDc4IiwicmRzIjoiUENfMTM4ODgwMTc5NDkyOTU1NzkwNTV8UFJPRF9QQ18xMzg4ODAxNzk0OTI5NTU3OTA1NSIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiMTM4ODgwMTc5NDkyOTU1NzkwNTUiLCJtaWQiOiI1NzY0NjI4Mjc3MDc3MjYyNTMiLCJwdnQiOiJoZyIsInV1bGUiOm51bGwsImdsIjoidXMiLCJobCI6ImVuIiwiZW5naW5lIjoiZ29vZ2xlX3Nob3BwaW5nX2xpZ2h0In0=",
          "serpapi_immersive_product_api": "https://serpapi.com/search.json?engine=google_immersive_product&page_token=eyJlaSI6bnVsbCwicHJvZHVjdGlkIjoiIiwiY2F0YWxvZ2lkIjoiMTY5MTgyOTA5NTczMTcyNTk0MDgiLCJoZWFkbGluZU9mZmVyRG9jaWQiOiI5MjU4MjYyMDQ3MzkzNzgxMDMxIiwiaW1hZ2VEb2NpZCI6IjEzNjQ1MDYwMTEzNzY0NzI4MDc4IiwicmRzIjoiUENfMTM4ODgwMTc5NDkyOTU1NzkwNTV8UFJPRF9QQ18xMzg4ODAxNzk0OTI5NTU3OTA1NSIsInF1ZXJ5IjoibWFjYm9vayIsImdwY2lkIjoiMTM4ODgwMTc5NDkyOTU1NzkwNTUiLCJtaWQiOiI1NzY0NjI4Mjc3MDc3MjYyNTMiLCJwdnQiOiJoZyIsInV1bGUiOm51bGwsImdsIjoidXMiLCJobCI6ImVuIiwiZW5naW5lIjoiZ29vZ2xlX3Nob3BwaW5nX2xpZ2h0In0%3D",
          "source": "Best Buy",
          "source_icon": "https://encrypted-tbn0.gstatic.com/favicon-tbn?q=tbn%3AANd9GcRJLrYt8ApvztGsW8TSy6-5HL7LwDNwH2emYmRabMUepMDXWE3LqD_Jltucg6NfE5z5MV57q9G1n_VVMyiUtZCVGXOuFlVA6g",
          "price": "$799.00",
          "extracted_price": 799,
          "old_price": "$999",
          "extracted_old_price": 999,
          "rating": 4.9,
          "reviews": 4800,
          "thumbnail": "https://encrypted-tbn2.gstatic.com/shopping?q=tbn:ANd9GcTOfjZa2vHN4_0Ab4CMs1nrqshtwaQgR7KwDwMcF1eSzvnx-VQnLNnm19kGrLOCgMKu34qrXsJPmJmiPZYYe9VCAsGVhWdQfK7WVIBOAk9oav96gmsnohihwA",
          "serpapi_thumbnail": "https://serpapi.com/images/url/eI-CBHicDclJDoIwAADAFyGCRFMSYypGlB01IF4MFmiRtCytVH2V3_E3Otf5fogQHTdVtWRoeHWiLBRxY_oEc5GLGk1QS1VO2q6rGV71y_-ZMCiAjU5hdb_k-rgLjOsU3gzL5xobek6EzGN8WLhyI3201crje2RPJYmZFzCqgcYevNDCvvuYGf1w5k5EHVpHlywrQWJBbickLeLKXaTJfh3CBrT5COaYctaSmkj4A8xKP5Y",
          "tag": "20% OFF",
          "extensions": [
            "20% OFF"
          ]
        },
        ...
      ]
    },
    ...
  ],
  "serpapi_pagination": {
    "next": "https://serpapi.com/search.json?device=desktop&engine=google_shopping_light&gl=us&google_domain=google.com&hl=en&q=macbook&start=10"
  }
}

```