# Amplify Fusion Enhanced Market News API

Enhanced contact API created in Amplify Fusion that demonstrates how to leverage the OpenAI API in a finance analysis example. The market news is retrieved from Finnhub.io's API using Fusion's HTTP/S Client Connector and enhanced using the OpenAI API and a prompt that provides the news response. The prompt provides the data and requests insights as illustrated below:

![Imgur](https://i.imgur.com/tqw9BPw.png)

* You can read more about how a similar prompt was engineered as well as the details of the OpenAI API call and response [here](https://gist.github.com/lbrenman/67ee78c716210448cb2605c8f5d6b2b7).
* The Open API Specification used to create the API in Fusion is in this repo in the file `marketnewsinsights.json` [here](https://github.com/lbrenman/AI-Enhanced-SFDC-Contact-Sales-Tool-API-in-Fusion/blob/master/enhancedcontact.json).
* The OpenAI AI POST body (prompt) is below:
    ```bash
    curl --location 'https://api.openai.com/v1/chat/completions' \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Bearer sk-p,,,,0A' \
    --data '{
    "model": "gpt-4-turbo",
    "messages": [
        {
        "role": "system",
        "content": "You are a financial analyst. Analyze the given market news data and provide insights in structured JSON format. Return only valid JSON — do not include explanations or anything outside the JSON object."
        },
        {
        "role": "user",
        "content": "Here is the latest market news data: [{\"category\":\"top news\",\"datetime\":1740856201,\"headline\":\"Michelin-star chef says this is the No. 1 thing home cooks waste money on: '\''It'\''s a vanity in the kitchen'\''\",\"id\":7453926,\"image\":\"https://image.cnbcfm.com/api/v1/image/103172592-GettyImages-187990397.jpg?v=1740768915\\u0026w=1920\\u0026h=1080\",\"related\":\"\",\"source\":\"CNBC\",\"summary\":\"Chef Gabriel Kreuther says one of the biggest mistakes he sees home cooks making is outfitting their kitchen as if they were running a restaurant.\",\"url\":\"https://www.cnbc.com/2025/03/01/michelin-star-chef-this-is-the-no-1-thing-home-cooks-waste-money-on.html\"},{\"category\":\"top news\",\"datetime\":1740848300,\"headline\":\"Buying small caps to find the next Nvidia can be risky. 5 questions to answer before starting\",\"id\":7453910,\"image\":\"https://image.cnbcfm.com/api/v1/image/108103855-1739921378874-108103855-1739907170185-JP3_8999.jpg?v=1739921426\\u0026w=1920\\u0026h=1080\",.............105470744-1537905608557ap_13050114030.jpg?v=1537905692\\u0026w=1920\\u0026h=1080\",\"related\":\"\",\"source\":\"CNBC\",\"summary\":\"American is under pressure to offer free in-flight internet after more airlines have begun offering the complimentary service.\",\"url\":\"https://www.cnbc.com/2025/02/28/american-airlines-free-inflight-wi-fi.html\"}]\n\nPlease analyze the data and return insights. Use the exact JSON structure below for the response:\n\n{\n  \"MarketSentiment\": [\n    {\n      \"category\": \"string\",\n      \"sentiment\": \"positive | negative | neutral\",\n      \"keyPoints\": [\"string\"]\n    }\n  ],\n  \"ConsumerBehaviorInsights\": [\n    {\n      \"trend\": \"string\",\n      \"impact\": \"high | medium | low\",\n      \"description\": \"string\"\n    }\n  ],\n  \"VolatilityAndInvestmentInsights\": [\n    {\n      \"assetClass\": \"string\",\n      \"volatility\": \"high | medium | low\",\n      \"investmentOpportunity\": \"string\",\n      \"riskLevel\": \"high | medium | low\"\n    }\n  ]\n}"
        }
    ],
    "temperature": 0.7
    }
    '
    ```
* The OpenAI API response is as follows:
    ```json
    {
    "id": "chatcmpl-B6dW0oBCtUSY1xkTSIwjG0kTJIMzH",
    "object": "chat.completion",
    "created": 1740921564,
    "model": "gpt-4-turbo-2024-04-09",
    "choices": [
        {
        "index": 0,
        "message": {
            "role": "assistant",
            "content": "{\n  \"MarketSentiment\": [\n    {\n      \"category\": \"real estate\",\n      \"sentiment\": \"negative\",\n      \"keyPoints\": [\n        \"Mortgage rates are falling without improving home sales.\",\n        \"Concerns about Trump's 'gold card' visa program possibly inflating the U.S. housing market.\"\n      ]\n    },\n    {\n      \"category\": \"cryptocurrency\",\n      \"sentiment\": \"negative\",\n      \"keyPoints\": [\n        \"Bitcoin experienced a significant selloff due to record ETF outflows.\"\n      ]\n    },\n    {\n      \"category\": \"equity\",\n      \"sentiment\": \"neutral\",\n      \"keyPoints\": [\n        \"U.S. stocks faced a rocky February with high macro uncertainty.\",\n        \"Nvidia stock struggles amidst market challenges.\"\n      ]\n    }\n  ],\n  \"ConsumerBehaviorInsights\": [\n    {\n      \"trend\": \"luxury kitchen investments\",\n      \"impact\": \"low\",\n      \"description\": \"Home cooks spending excessively on professional kitchen setups is seen as unnecessary vanity.\"\n    },\n    {\n      \"trend\": \"retirement concerns\",\n      \"impact\": \"medium\",\n      \"description\": \"Individuals express growing worries about financial security and retirement planning.\"\n    }\n  ],\n  \"VolatilityAndInvestmentInsights\": [\n    {\n      \"assetClass\": \"small caps\",\n      \"volatility\": \"high\",\n      \"investmentOpportunity\": \"potential for significant growth\",\n      \"riskLevel\": \"high\"\n    },\n    {\n      \"assetClass\": \"cryptocurrency\",\n      \"volatility\": \"high\",\n      \"investmentOpportunity\": \"market correction could provide buying opportunities\",\n      \"riskLevel\": \"high\"\n    },\n    {\n      \"assetClass\": \"real estate\",\n      \"volatility\": \"medium\",\n      \"investmentOpportunity\": \"uncertainty around visa policies could affect market prices\",\n      \"riskLevel\": \"medium\"\n    }\n  ]\n}",
            "refusal": null
        },
        "logprobs": null,
        "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 3876,
        "completion_tokens": 405,
        "total_tokens": 4281,
        "prompt_tokens_details": {
        "cached_tokens": 0,
        "audio_tokens": 0
        },
        "completion_tokens_details": {
        "reasoning_tokens": 0,
        "audio_tokens": 0,
        "accepted_prediction_tokens": 0,
        "rejected_prediction_tokens": 0
        }
    },
    "service_tier": "default",
    "system_fingerprint": "fp_7c63087da1"
    }
    ```
* You can see the API in action in a sample Web app [here]()
* Some screen shots from the Fusion project are shown below:
![Imgur](https://i.imgur.com/txk7hTZ.png)
![Imgur](https://i.imgur.com/y0Y6Yag.png)
![Imgur](https://i.imgur.com/se5hOw3.png)
![Imgur](https://i.imgur.com/RYLpCjS.png)
![Imgur](https://i.imgur.com/eKAvLu4.png)
![Imgur](https://i.imgur.com/tHXR7E7.png)