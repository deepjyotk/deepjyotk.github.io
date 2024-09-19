---
layout: page
title: Travel Insights
description: Explored the performance differences between Java 21's new virtual threads and the traditional platform threads in a travel planning application. The system handles services such as trip reservations, event planning, accommodation recommendations, and local recommendations.
img: assets/img/projects/travel-insights/image.png
importance: 3
category: fun
related_publications: false
---

#### 🔗[Github Link](https://github.com/deepjyotk/trade-stream)

    Technologies Used: Java21, Virtual Thread, Multithreading

### Key Objectives

1. Scalability Testing: Evaluating how the system performs under increasing concurrent user loads.
2. Threading Model: Comparing results between virtual threads (introduced in Java 21) and platform threads (older version of Java).
3. Performance Metrics: Throughput (transactions per second) and Response Time.

### Setup and Testing

For the purpose of testing, the following services were used:

1. Trip Reservation: Two external service calls (flight search and reservation) were made in sequence.
2. Trip Plan: Four parallel tasks (event search, weather check, accommodation, and transportation recommendations) were executed using both platform and virtual threads.

#### The scalability test was carried out using JMeter. The goal was to evaluate:

1. Throughput: The number of concurrent transactions the system can handle.
2. Response Time: The time taken to process each transaction.

## Results

### 1. Platform Threads

- At 300 concurrent users, throughput remained capped after 200 users due to Tomcat's platform thread limit.
- Response time increased significantly after hitting the thread limit, causing a delay in processing queued requests.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/platform/aggregate-report.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/platform/throughput.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/platform/response-time.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   Performance for Platform Threads: 
   Left: Aggregate Report, Middle: Throughput (Transactions/second), Right: Response Time Over Time
</div>

### 2. Virtual Threads

- Virtual threads allowed the application to handle more concurrent users without the steep rise in response time, as it doesn't hit the same hard limit of threads in Tomcat.
- Both throughput and response time were more stable compared to platform threads.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/virtual/aggregate-report.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/virtual/throughput.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/travel-insights/virtual/response-time.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   Performance for Virtual Threads: 
   Left: Aggregate Report, Middle: Throughput (Transactions/second), Right: Response Time Over Time</div>

## Conclusion

The introduction of virtual threads in Java 21 offers substantial scalability improvements in handling concurrent workloads, particularly for IO-bound tasks like trip planning services. The ability to scale efficiently without increasing the response time drastically makes virtual threads a preferable choice in modern web applications.

### Motivation

I built this project to explore the performance improvements brought by Java 21's virtual threads, particularly in handling concurrent workloads more efficiently. My goal was to understand how these new threads can enhance scalability and responsiveness in real-world applications like travel planning systems.
