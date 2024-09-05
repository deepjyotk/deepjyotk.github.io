---
layout: page
title: TradeStream
description: Trade Stream is a gRPC-based trading platform that allows users to execute stock trades and receive real-time price updates with high efficiency and low latency.
img: assets/img/projects/trade-stream/ui.png
importance: 2
category: fun
related_publications: false
---

#### 🔗[Github Link](https://github.com/deepjyotk/trade-stream)

    Technologies Used: Spring Boot, gRPC, H2 DB, JPA

### Features

1. Real-Time Stock Trading: Enables users to buy and sell stocks seamlessly, with instant price retrieval and trade execution.
2. Live Price Updates: Provides continuous streaming of real-time stock price updates, allowing users to monitor market fluctuations instantly.
3. User-Centric Design: Supports a smooth user experience by handling all backend processes, including price fetching and balance updates, without requiring frontend input for pricing.
4. Scalable gRPC Architecture: Leverages gRPC for efficient, low-latency communication between microservices, ensuring quick and reliable data transmission.
<div class="row">
    <div class="col-sm-12">
        {% include figure.liquid loading="eager" path="assets/img/projects/trade-stream/ui.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Trade Stream's intuitive dashboard allows users to view real-time stock prices, manage their portfolio, and execute buy or sell actions seamlessly.
</div>

### Make Trade - Architecture

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/trade-stream/make-trade-arch.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Stock Trading Service
</div>

The stock trading service in "Trade Stream" enables users to buy and sell stocks through a streamlined gRPC-based communication system. The service is designed to interact with multiple microservices to ensure accurate price fetching, secure trading, and responsive feedback to the user.

**Architecture Explanation:**

1. **User Request Initiation:**

   - The process starts when a user sends a trade request to the **aggregator-service** via the `/trade` endpoint. The request contains crucial information such as the `user_id`, `ticker`, `quantity`, and the action (`BUY` or `SELL`).

2. **Price Fetching:**

   - Since the price is not directly passed from the frontend, the **aggregator-service** first interacts with the **stock-service** to fetch the current price of the stock. This is done through a synchronous gRPC call using the `stockServiceBlockingStub.getStockPrice` method, passing a `StockPriceRequest` that includes the stock's `ticker`.

   - The **stock-service** processes the `StockPriceRequest` and returns the stock's current price, which is then used by the **aggregator-service** to complete the trade.

3. **Trade Execution:**

   - With the fetched price, the **aggregator-service** constructs a `StockTradeRequest` and invokes the `stockServiceStub.tradeStock` method. This gRPC call triggers the actual trade process, which involves updating user data and the stock inventory in the **user-service**.

   - The **user-service** processes the trade by adjusting the user’s balance and stock holdings according to the action (`BUY` or `SELL`), and returns a `StockTradeResponse` to the **aggregator-service**. This response contains the updated details, including the total price of the trade and the user's remaining balance.

4. **Response to User:**
   - Finally, the **aggregator-service** sends a `StockTradeResponse` back to the user, confirming the success of the transaction along with details such as the trade price, total cost, and updated balance.

**Key Protobuf Definitions:**

- `StockTradeRequest`: Contains fields like `user_id`, `ticker`, `price`, `quantity`, and `TradeAction` (either `BUY` or `SELL`).
- `TradeAction`: Enum defining the possible actions (`BUY` or `SELL`).
- `StockTradeResponse`: Returns the trade details, including total price and updated balance.

### Price Update Streaming- Architecture

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/trade-stream/price-updates-arch.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Price Update Streaming
</div>

The stock trading service in "Trade Stream" enables users to buy and sell stocks through a streamlined gRPC-based communication system. The service is designed to interact with multiple microservices to ensure accurate price fetching, secure trading, and responsive feedback to the user.

**Architecture Explanation:**

1. **User Request Initiation:**

   - The process starts when a user sends a trade request to the **aggregator-service** via the `/trade` endpoint. The request contains crucial information such as the `user_id`, `ticker`, `quantity`, and the action (`BUY` or `SELL`).

2. **Price Fetching:**

   - Since the price is not directly passed from the frontend, the **aggregator-service** first interacts with the **stock-service** to fetch the current price of the stock. This is done through a synchronous gRPC call using the `stockServiceBlockingStub.getStockPrice` method, passing a `StockPriceRequest` that includes the stock's `ticker`.

   - The **stock-service** processes the `StockPriceRequest` and returns the stock's current price, which is then used by the **aggregator-service** to complete the trade.

3. **Trade Execution:**

   - With the fetched price, the **aggregator-service** constructs a `StockTradeRequest` and invokes the `stockServiceStub.tradeStock` method. This gRPC call triggers the actual trade process, which involves updating user data and the stock inventory in the **user-service**.

   - The **user-service** processes the trade by adjusting the user’s balance and stock holdings according to the action (`BUY` or `SELL`), and returns a `StockTradeResponse` to the **aggregator-service**. This response contains the updated details, including the total price of the trade and the user's remaining balance.

4. **Response to User:**
   - Finally, the **aggregator-service** sends a `StockTradeResponse` back to the user, confirming the success of the transaction along with details such as the trade price, total cost, and updated balance.

**Key Protobuf Definitions:**

- `StockTradeRequest`: Contains fields like `user_id`, `ticker`, `price`, `quantity`, and `TradeAction` (either `BUY` or `SELL`).
- `TradeAction`: Enum defining the possible actions (`BUY` or `SELL`).
- `StockTradeResponse`: Returns the trade details, including total price and updated balance.

### Motivation

The motivation behind the Trade Stream project was to empower individual investors by providing them with a real-time trading platform that combines ease of use with powerful functionality. Additionally, it served as a learning opportunity to explore and implement gRPC and microservices for efficient, scalable communication in financial applications.
