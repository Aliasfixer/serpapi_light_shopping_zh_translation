# Google Shopping Light API

SerpApi的Google Shopping Light API可以让你极高速度抓取Google Shopping的结果。Google Shopping Light引擎仅保留最核心的数据，不包含常规Google Shopping页面中能获取的额外信息，相比标准的[Google Shopping API](https://serpapi.com/google-shopping-api)它能够提供更快的响应速度。

该 API 可通过以下端点进行访问：/search?engine=google_shopping。

你可以通过发送 GET 请求查询：https://serpapi.com/search?engine=google_shopping&q=coffee 或者您可以前往[Playground](https://serpapi.com/playground?engine=google_shopping)体验实时、可交互的官方演示。

## API 调用参数

1. **查询关键字**

| 参数名       | 类型     | 必填 | 描述                           |
| ------------ | -------- | ---- | ------------------------------ |
| q            | string   | 强制要求   | 本参数定义搜索的关键字，你可以定义任何你希望在Google Shopping search中搜索的内容。|

2. **地理位置**

|参数名| 类型     | 必填 | 描述                                                                                                                                                                                                                                        |
|---------|--------|----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|location| string | 可选 | 本参数定义你希望搜索发起的地理位置，如果有多个地理位置符合请求，我们会选取最多请求数的地理位置。<br>在[/locations.json API](https://serpapi.com/locations-api)查看更多关于控制精准地理位置请求的信息，<br>"location"参数与"uule"参数不能同时使用，建议使用"location"参数将位置信息指定到城市级别以模拟真实用户请求。如果"location"参数未指定位置，搜索将可能使用代理服务器所在的位置。 |
|uule| string | 可选 | 本参数是Google加密的位置信息，"uule"与"location"参数不能同时使用。                                                                                                                                                                                              |


3. **本地化**
- "google_domain"(可选): 本参数定义Google使用的域名，默认为 google.com，查看[Google domains](https://serpapi.com/google-domains)获取受支持的Google域名完整列表。

- "gl"(可选): 本参数定义Google搜索使用的国家。这个参数是一个两个字符的国家代码(例如：美国为us，英国为uk，法国为fr)，查看[Google Shopping countries](https://serpapi.com/google-shopping-countries)获取受支持的国家完整列表。

- "hl"(可选): 本参数定义Google搜索的语言，这个参数是一个两个参数的语言代码(例如：英语为en，简体中文为zh-cn，zh-tw为繁体中文)，查看[Google languages](https://serpapi.com/google-languages)获取受支持的语言完整列表。

|参数名| 类型     | 必填 | 描述                                                                                                                                                      |
|---------|--------|----|---------------------------------------------------------------------------------------------------------------------------------------------------------|
|google_domain| string | 可选 | 本参数定义Google使用的域名，默认为 google.com，查看[Google domains](https://serpapi.com/google-domains)获取受支持的Google域名完整列表。                                               |
|gl| string | 可选 | 本参数定义Google搜索使用的国家。这个参数是一个两个字符的国家代码(例如：美国为us，英国为uk，法国为fr)。<br>查看[Google Shopping countries](https://serpapi.com/google-shopping-countries)获取受支持的国家完整列表。 |
4. **高级过滤器**
- "shoprs"(可选): 本参数定义一个包含查询及搜索过滤器相关metadata的token。"q"参数与"shoprs"并不是必须同时使用。如果要应用多个过滤器，可以使用"||"连接，比如 shoprs_1||shoprs_2||shoprs_3。该参数的可用值无法通过 Google Shopping Light API 获取。你可以使用我们的 [Google Shopping API](https://serpapi.com/google-shopping-api) 来获取这些值，或者直接访问 Google Shopping 网站，设置你需要的过滤条件，然后将其 URL 中的 shoprs 值复制到 SerpApi 的 URL 中即可。

- "min_price"(可选): 本参数定义最低价格。(本参数会覆盖"shoprs"参数中所包含的对应过滤器)

-