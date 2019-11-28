# WSO2 API Manager Performance Test Results : Oauth tokens

During each release, we execute various automated performance test scenarios and publish the results.

| Test Scenarios | Description |
| --- | --- |
| Passthrough | A secured API, which directly invokes the back-end service. |
| Transformation | A secured API, which has a mediation extension to modify the message. |

Our test client is [Apache JMeter](https://jmeter.apache.org/index.html). We test each scenario for a fixed duration of
time. We split the test results into warmup and measurement parts and use the measurement part to compute the
performance metrics.

Test scenarios use a [Netty](https://netty.io/) based back-end service which echoes back any request
posted to it after a specified period of time.

We run the performance tests under different numbers of concurrent users, message sizes (payloads) and back-end service
delays.

The main performance metrics:

1. **Throughput**: The number of requests that the WSO2 API Manager processes during a specific time interval (e.g. per second).
2. **Response Time**: The end-to-end latency for an operation of invoking an API. The complete distribution of response times was recorded.

In addition to the above metrics, we measure the load average and several memory-related metrics.

The following are the test parameters.

| Test Parameter | Description | Values |
| --- | --- | --- |
| Scenario Name | The name of the test scenario. | Refer to the above table. |
| Heap Size | The amount of memory allocated to the application | 4G |
| Concurrent Users | The number of users accessing the application at the same time. | 50, 100, 200, 300, 500, 1000 |
| Message Size (Bytes) | The request payload size in Bytes. | 50, 1024, 10240 |
| Back-end Delay (ms) | The delay added by the back-end service. | 0, 30, 500, 1000 |

The duration of each test is **900 seconds**. The warm-up period is **300 seconds**.
The measurement results are collected after the warm-up period.

A [**m5.large** Amazon EC2 instance](https://aws.amazon.com/ec2/instance-types/) was used to install WSO2 API Manager.

The following are the measurements collected from each performance test conducted for a given combination of
test parameters.

| Measurement | Description |
| --- | --- |
| Error % | Percentage of requests with errors |
| Average Response Time (ms) | The average response time of a set of results |
| Standard Deviation of Response Time (ms) | The “Standard Deviation” of the response time. |
| 99th Percentile of Response Time (ms) | 99% of the requests took no more than this time. The remaining samples took at least as long as this |
| Throughput (Requests/sec) | The throughput measured in requests per second. |
| Average Memory Footprint After Full GC (M) | The average memory consumed by the application after a full garbage collection event. |

The following is the summary of performance test results collected for the measurement period.

|  Scenario Name | Heap Size | Concurrent Users | Message Size (Bytes) | Back-end Service Delay (ms) | Error % | Throughput (Requests/sec) | Average Response Time (ms) | Standard Deviation of Response Time (ms) | 99th Percentile of Response Time (ms) | WSO2 API Manager GC Throughput (%) | Average WSO2 API Manager Memory Footprint After Full GC (M) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
|  Passthrough | 4G | 50 | 50 | 0 | 0 | 3579.41 | 13.9 | 26.22 | 67 | 94.16 | 277.149 |
|  Passthrough | 4G | 50 | 50 | 30 | 0 | 1508.47 | 33.08 | 35.59 | 45 | 96.64 | 72.222 |
|  Passthrough | 4G | 50 | 50 | 500 | 0 | 99.49 | 502.8 | 4.66 | 507 | 99.54 | 73.348 |
|  Passthrough | 4G | 50 | 50 | 1000 | 0 | 49.82 | 1002.68 | 4.57 | 1011 | 99.6 | 72.598 |
|  Passthrough | 4G | 50 | 1024 | 0 | 0 | 3480.83 | 14.29 | 27.5 | 56 | 94.02 | 316.106 |
|  Passthrough | 4G | 50 | 1024 | 30 | 0 | 1513.58 | 32.96 | 14.18 | 44 | 96.59 | 72.363 |
|  Passthrough | 4G | 50 | 1024 | 500 | 0 | 99.53 | 502.5 | 4.75 | 505 | 99.55 | 72.7 |
|  Passthrough | 4G | 50 | 1024 | 1000 | 0 | 49.83 | 1002.68 | 5.07 | 1007 | 99.6 | 72.058 |
|  Passthrough | 4G | 50 | 10240 | 0 | 0 | 2036.46 | 24.47 | 27.17 | 63 | 96.02 | 237.863 |
|  Passthrough | 4G | 50 | 10240 | 30 | 0 | 1441.36 | 34.61 | 14.61 | 58 | 96.5 | 72.536 |
|  Passthrough | 4G | 50 | 10240 | 500 | 0 | 99.44 | 503 | 4.29 | 507 | 99.54 | 73.573 |
|  Passthrough | 4G | 50 | 10240 | 1000 | 0 | 49.79 | 1002.3 | 3.12 | 1007 | 99.6 | 74.038 |
|  Passthrough | 4G | 100 | 50 | 0 | 0 | 3786.84 | 26.33 | 36.15 | 122 | 93.78 | 304.913 |
|  Passthrough | 4G | 100 | 50 | 30 | 0 | 2760.85 | 36.15 | 35.47 | 104 | 95.22 | 294.574 |
|  Passthrough | 4G | 100 | 50 | 500 | 0 | 198.95 | 502.29 | 5.21 | 507 | 99.44 | 72.88 |
|  Passthrough | 4G | 100 | 50 | 1000 | 0 | 99.58 | 1002.62 | 5.19 | 1011 | 99.52 | 72.713 |
|  Passthrough | 4G | 100 | 1024 | 0 | 0 | 3571.14 | 27.92 | 38.31 | 119 | 94.07 | 301.177 |
|  Passthrough | 4G | 100 | 1024 | 30 | 0 | 2737.61 | 36.45 | 32.74 | 101 | 95.17 | 270.192 |
|  Passthrough | 4G | 100 | 1024 | 500 | 0 | 199.1 | 502.32 | 3.94 | 505 | 99.45 | 73.181 |
|  Passthrough | 4G | 100 | 1024 | 1000 | 0 | 99.6 | 1002.93 | 6.44 | 1011 | 99.5 | 72.746 |
|  Passthrough | 4G | 100 | 10240 | 0 | 0 | 1997.77 | 49.97 | 39.46 | 161 | 95.51 | 251.291 |
|  Passthrough | 4G | 100 | 10240 | 30 | 0 | 1986.1 | 50.24 | 34 | 156 | 95.84 | 228.625 |
|  Passthrough | 4G | 100 | 10240 | 500 | 0 | 198.71 | 503.27 | 4.41 | 515 | 99.46 | 72.623 |
|  Passthrough | 4G | 100 | 10240 | 1000 | 0 | 99.57 | 1002.63 | 5.25 | 1011 | 99.52 | 73.2 |
|  Passthrough | 4G | 200 | 50 | 0 | 0 | 3861.66 | 51.7 | 48.03 | 209 | 93.81 | 289.615 |
|  Passthrough | 4G | 200 | 50 | 30 | 0 | 3614.21 | 55.24 | 53.35 | 206 | 93.73 | 336.493 |
|  Passthrough | 4G | 200 | 50 | 500 | 0 | 397.99 | 502.67 | 5.12 | 511 | 99.24 | 72.739 |
|  Passthrough | 4G | 200 | 50 | 1000 | 0 | 199.03 | 1002.53 | 5.61 | 1011 | 99.42 | 72.179 |
|  Passthrough | 4G | 200 | 1024 | 0 | 0 | 3516.47 | 56.79 | 55.6 | 215 | 94.17 | 332.038 |
|  Passthrough | 4G | 200 | 1024 | 30 | 0 | 3362.76 | 59.39 | 57.84 | 209 | 94.07 | 347.269 |
|  Passthrough | 4G | 200 | 1024 | 500 | 0 | 397.74 | 502.86 | 5.59 | 515 | 99.19 | 72.055 |
|  Passthrough | 4G | 200 | 1024 | 1000 | 0 | 199.2 | 1002.51 | 4.79 | 1011 | 99.44 | 73.208 |
|  Passthrough | 4G | 200 | 10240 | 0 | 0 | 1976.44 | 101.09 | 55.2 | 247 | 95.92 | 235.961 |
|  Passthrough | 4G | 200 | 10240 | 30 | 0 | 1991.78 | 100.29 | 50.41 | 263 | 95.44 | 198.219 |
|  Passthrough | 4G | 200 | 10240 | 500 | 0 | 397.03 | 503.78 | 6.73 | 531 | 99.15 | 72.82 |
|  Passthrough | 4G | 200 | 10240 | 1000 | 0 | 198.96 | 1002.79 | 4.97 | 1015 | 99.4 | 72.496 |
|  Passthrough | 4G | 300 | 50 | 0 | 0 | 3707.96 | 80.81 | 74.34 | 263 | 93.84 | 344.342 |
|  Passthrough | 4G | 300 | 50 | 30 | 0 | 3692.82 | 81.13 | 67.03 | 247 | 93.8 | 334.444 |
|  Passthrough | 4G | 300 | 50 | 500 | 0 | 595.91 | 503.39 | 8.45 | 527 | 98.91 | 72.838 |
|  Passthrough | 4G | 300 | 50 | 1000 | 0 | 298.53 | 1002.76 | 6.13 | 1015 | 99.31 | 72.894 |
|  Passthrough | 4G | 300 | 1024 | 0 | 0 | 3606.35 | 83.07 | 71.53 | 263 | 93.85 | 340.989 |
|  Passthrough | 4G | 300 | 1024 | 30 | 0 | 3418.74 | 87.65 | 73.99 | 251 | 93.93 | 384.685 |
|  Passthrough | 4G | 300 | 1024 | 500 | 0 | 595.76 | 503.51 | 8.73 | 531 | 98.9 | 73.518 |
|  Passthrough | 4G | 300 | 1024 | 1000 | 0 | 298.82 | 1002.95 | 8.26 | 1019 | 99.32 | 72.03 |
|  Passthrough | 4G | 300 | 10240 | 0 | 0 | 1986.45 | 150.91 | 70.01 | 349 | 95.73 | 220.58 |
|  Passthrough | 4G | 300 | 10240 | 30 | 0 | 2030.73 | 147.6 | 73.62 | 331 | 95.55 | 259.453 |
|  Passthrough | 4G | 300 | 10240 | 500 | 0 | 594.12 | 504.93 | 10.36 | 551 | 98.8 | 72.526 |
|  Passthrough | 4G | 300 | 10240 | 1000 | 0 | 298.64 | 1002.77 | 17.77 | 1015 | 99.27 | 72.27 |
|  Passthrough | 4G | 500 | 50 | 0 | 0 | 3891.58 | 128.37 | 84.73 | 347 | 93.56 | 375.482 |
|  Passthrough | 4G | 500 | 50 | 30 | 0 | 3794.07 | 131.68 | 81.33 | 335 | 93.52 | 395.28 |
|  Passthrough | 4G | 500 | 50 | 500 | 0 | 986.63 | 506.69 | 16.87 | 603 | 98.1 | 72.2 |
|  Passthrough | 4G | 500 | 50 | 1000 | 0 | 497.29 | 1003.03 | 7.78 | 1023 | 98.98 | 71.54 |
|  Passthrough | 4G | 500 | 1024 | 0 | 0 | 3617.32 | 138.03 | 100.34 | 361 | 93.6 | 360.877 |
|  Passthrough | 4G | 500 | 1024 | 30 | 0 | 3555.67 | 140.52 | 82.64 | 347 | 93.85 | 380.036 |
|  Passthrough | 4G | 500 | 1024 | 500 | 0 | 985.95 | 506.95 | 16.83 | 599 | 98.11 | 71.925 |
|  Passthrough | 4G | 500 | 1024 | 1000 | 0 | 497.51 | 1003.41 | 8.15 | 1039 | 99.02 | 73.778 |
|  Passthrough | 4G | 500 | 10240 | 0 | 0 | 1984.17 | 252.01 | 87.98 | 511 | 95.49 | 194.974 |
|  Passthrough | 4G | 500 | 10240 | 30 | 0 | 1991.05 | 251.14 | 102.38 | 481 | 95.95 | 282.789 |
|  Passthrough | 4G | 500 | 10240 | 500 | 0 | 971.54 | 514.55 | 27.1 | 647 | 97.83 | 72.356 |
|  Passthrough | 4G | 500 | 10240 | 1000 | 0 | 497.36 | 1003.66 | 8.61 | 1039 | 98.92 | 72.495 |
|  Passthrough | 4G | 1000 | 50 | 0 | 0 | 3870.17 | 258.31 | 159.82 | 575 | 92.78 | 436.828 |
|  Passthrough | 4G | 1000 | 50 | 30 | 0 | 3902.75 | 256.17 | 134.03 | 559 | 92.93 | 400.482 |
|  Passthrough | 4G | 1000 | 50 | 500 | 0 | 1900.91 | 525.8 | 89.08 | 711 | 95.53 | 313.608 |
|  Passthrough | 4G | 1000 | 50 | 1000 | 0 | 990.39 | 1008.02 | 20.01 | 1119 | 97.88 | 71.685 |
|  Passthrough | 4G | 1000 | 1024 | 0 | 0 | 3472.2 | 287.99 | 146.53 | 623 | 93.53 | 444.184 |
|  Passthrough | 4G | 1000 | 1024 | 30 | 0 | 3595.61 | 278.08 | 144.16 | 591 | 93.41 | 399.582 |
|  Passthrough | 4G | 1000 | 1024 | 500 | 0 | 1902.89 | 525.19 | 76.54 | 707 | 95.85 | 288.986 |
|  Passthrough | 4G | 1000 | 1024 | 1000 | 0 | 989.85 | 1008.35 | 19.97 | 1119 | 97.82 | 72.131 |
|  Passthrough | 4G | 1000 | 10240 | 0 | 0 | 1994.15 | 501.5 | 140.78 | 887 | 96.03 | 313.191 |
|  Passthrough | 4G | 1000 | 10240 | 30 | 0 | 1940.44 | 515.37 | 141.44 | 839 | 96.03 | 306.234 |
|  Passthrough | 4G | 1000 | 10240 | 500 | 0 | 1696.43 | 589.05 | 104.97 | 895 | 95.88 | 246.749 |
|  Passthrough | 4G | 1000 | 10240 | 1000 | 0 | 976.58 | 1022.08 | 37.54 | 1191 | 97.6 | 71.7 |
|  Transformation | 4G | 50 | 50 | 0 | 0 | 2785.38 | 17.87 | 23.54 | 98 | 94.65 | 279.141 |
|  Transformation | 4G | 50 | 50 | 30 | 0 | 1460.5 | 34.17 | 20.24 | 96 | 95.94 | 170.738 |
|  Transformation | 4G | 50 | 50 | 500 | 0 | 99.39 | 503.24 | 4.23 | 515 | 99.49 | 72.077 |
|  Transformation | 4G | 50 | 50 | 1000 | 0 | 49.82 | 1003.41 | 7.63 | 1011 | 99.55 | 72.808 |
|  Transformation | 4G | 50 | 1024 | 0 | 0 | 2207.46 | 22.58 | 23.01 | 97 | 95.34 | 227.566 |
|  Transformation | 4G | 50 | 1024 | 30 | 0 | 1362.88 | 36.62 | 19.49 | 104 | 95.93 | 162.465 |
|  Transformation | 4G | 50 | 1024 | 500 | 0 | 99.42 | 503.22 | 4.39 | 511 | 99.47 | 72.941 |
|  Transformation | 4G | 50 | 1024 | 1000 | 0 | 49.78 | 1002.97 | 5.72 | 1011 | 99.54 | 73.408 |
|  Transformation | 4G | 50 | 10240 | 0 | 0 | 724.25 | 68.91 | 37.37 | 183 | 95.49 | 118.513 |
|  Transformation | 4G | 50 | 10240 | 30 | 0 | 642.23 | 77.73 | 25.9 | 176 | 95.6 | 71.93 |
|  Transformation | 4G | 50 | 10240 | 500 | 0 | 98.25 | 508.89 | 7.48 | 539 | 99.29 | 71.866 |
|  Transformation | 4G | 50 | 10240 | 1000 | 0 | 49.61 | 1006.5 | 5.22 | 1031 | 99.47 | 73.602 |
|  Transformation | 4G | 100 | 50 | 0 | 0 | 2855.17 | 34.94 | 31.4 | 138 | 94.74 | 229.124 |
|  Transformation | 4G | 100 | 50 | 30 | 0 | 2336 | 42.72 | 22.98 | 126 | 95.58 | 215.615 |
|  Transformation | 4G | 100 | 50 | 500 | 0 | 198.74 | 503.07 | 19.94 | 515 | 99.32 | 72.12 |
|  Transformation | 4G | 100 | 50 | 1000 | 0 | 99.62 | 1002.7 | 5.02 | 1011 | 99.48 | 73.244 |
|  Transformation | 4G | 100 | 1024 | 0 | 0 | 2278.3 | 43.8 | 35.23 | 141 | 95.22 | 247.323 |
|  Transformation | 4G | 100 | 1024 | 30 | 0 | 1932.76 | 51.65 | 28.76 | 127 | 95.74 | 209.411 |
|  Transformation | 4G | 100 | 1024 | 500 | 0 | 198.71 | 503.41 | 4.33 | 515 | 99.27 | 73.12 |
|  Transformation | 4G | 100 | 1024 | 1000 | 0 | 99.58 | 1003.75 | 8.23 | 1039 | 99.45 | 73.137 |
|  Transformation | 4G | 100 | 10240 | 0 | 0 | 718.02 | 139.15 | 64.28 | 317 | 95.65 | 118.446 |
|  Transformation | 4G | 100 | 10240 | 30 | 0 | 713.78 | 139.93 | 48.93 | 275 | 95.71 | 115.043 |
|  Transformation | 4G | 100 | 10240 | 500 | 0 | 193.7 | 516.3 | 15.34 | 579 | 98.85 | 72.092 |
|  Transformation | 4G | 100 | 10240 | 1000 | 0 | 98.96 | 1008.78 | 8.02 | 1047 | 99.26 | 72.976 |
|  Transformation | 4G | 200 | 50 | 0 | 0 | 2888.2 | 69.14 | 46.08 | 203 | 94.49 | 246.233 |
|  Transformation | 4G | 200 | 50 | 30 | 0 | 2750.51 | 72.6 | 42.25 | 182 | 94.64 | 253.669 |
|  Transformation | 4G | 200 | 50 | 500 | 0 | 396.87 | 503.89 | 7.88 | 535 | 98.87 | 73.879 |
|  Transformation | 4G | 200 | 50 | 1000 | 0 | 199.18 | 1003.34 | 7.13 | 1031 | 99.28 | 74.007 |
|  Transformation | 4G | 200 | 1024 | 0 | 0 | 2295.58 | 87.02 | 49.78 | 228 | 95.25 | 214.991 |
|  Transformation | 4G | 200 | 1024 | 30 | 0 | 2199.77 | 90.81 | 49.03 | 201 | 95.13 | 259.658 |
|  Transformation | 4G | 200 | 1024 | 500 | 0 | 396.06 | 504.94 | 8.14 | 547 | 98.78 | 73.133 |
|  Transformation | 4G | 200 | 1024 | 1000 | 0 | 199.15 | 1003.15 | 17.36 | 1015 | 99.22 | 72.761 |
|  Transformation | 4G | 200 | 10240 | 0 | 0 | 714.66 | 279.92 | 108.86 | 579 | 95.9 | 121.841 |
|  Transformation | 4G | 200 | 10240 | 30 | 0 | 701.91 | 285.01 | 99.92 | 547 | 95.65 | 120.179 |
|  Transformation | 4G | 200 | 10240 | 500 | 0 | 345.35 | 578.57 | 66.56 | 759 | 97.88 | 72.953 |
|  Transformation | 4G | 200 | 10240 | 1000 | 0 | 196.3 | 1017.52 | 17.8 | 1087 | 98.8 | 73.236 |
|  Transformation | 4G | 300 | 50 | 0 | 0 | 2868.5 | 104.47 | 62.64 | 277 | 94.43 | 266.273 |
|  Transformation | 4G | 300 | 50 | 30 | 0 | 2766.63 | 108.31 | 53.33 | 248 | 94.55 | 260.811 |
|  Transformation | 4G | 300 | 50 | 500 | 0 | 592.39 | 506.34 | 13.06 | 579 | 98.34 | 72.3 |
|  Transformation | 4G | 300 | 50 | 1000 | 0 | 298.62 | 1002.95 | 5.6 | 1023 | 99.11 | 72.873 |
|  Transformation | 4G | 300 | 1024 | 0 | 0 | 2315.37 | 129.47 | 68.95 | 315 | 94.94 | 233.275 |
|  Transformation | 4G | 300 | 1024 | 30 | 0 | 2284.01 | 131.22 | 52.81 | 281 | 95.11 | 230.446 |
|  Transformation | 4G | 300 | 1024 | 500 | 0 | 586.77 | 511.23 | 17.51 | 595 | 98.06 | 72.135 |
|  Transformation | 4G | 300 | 1024 | 1000 | 0 | 298.24 | 1004.31 | 7.65 | 1039 | 98.97 | 73.451 |
|  Transformation | 4G | 300 | 10240 | 0 | 0 | 718.78 | 417.52 | 140.52 | 799 | 95.88 | 127.882 |
|  Transformation | 4G | 300 | 10240 | 30 | 0 | 710.62 | 422.24 | 136.5 | 767 | 95.49 | 123.012 |
|  Transformation | 4G | 300 | 10240 | 500 | 0 | 406.33 | 737.81 | 121.63 | 963 | 97.12 | 73.141 |
|  Transformation | 4G | 300 | 10240 | 1000 | 0 | 270.31 | 1108.13 | 101.03 | 1367 | 98.28 | 72.325 |
|  Transformation | 4G | 500 | 50 | 0 | 0 | 2863.47 | 174.51 | 109.16 | 405 | 93.66 | 376.253 |
|  Transformation | 4G | 500 | 50 | 30 | 0 | 2898.7 | 172.39 | 104.27 | 377 | 93.38 | 398.531 |
|  Transformation | 4G | 500 | 50 | 500 | 0 | 962.37 | 519.35 | 30.95 | 659 | 96.65 | 73.208 |
|  Transformation | 4G | 500 | 50 | 1000 | 0 | 494.71 | 1009.07 | 16.72 | 1095 | 98.53 | 72.18 |
|  Transformation | 4G | 500 | 1024 | 0 | 0 | 2305.53 | 216.76 | 114.57 | 469 | 94.23 | 332.229 |
|  Transformation | 4G | 500 | 1024 | 30 | 0 | 2295.26 | 217.8 | 99.4 | 449 | 94.23 | 314.758 |
|  Transformation | 4G | 500 | 1024 | 500 | 0 | 933.35 | 535.52 | 43.92 | 707 | 96.12 | 73.304 |
|  Transformation | 4G | 500 | 1024 | 1000 | 0 | 493.82 | 1010.89 | 19.57 | 1103 | 98.23 | 72.874 |
|  Transformation | 4G | 500 | 10240 | 0 | 0 | 712.37 | 701.53 | 194.7 | 1207 | 95.56 | 135.002 |
|  Transformation | 4G | 500 | 10240 | 30 | 0 | 716.56 | 697.42 | 187.17 | 1183 | 95.95 | 132.587 |
|  Transformation | 4G | 500 | 10240 | 500 | 0 | 512.76 | 974.35 | 192.78 | 1335 | 95.64 | 73.212 |
|  Transformation | 4G | 500 | 10240 | 1000 | 0 | 375.3 | 1331.13 | 204.62 | 1719 | 97.2 | 72.625 |
|  Transformation | 4G | 1000 | 50 | 0 | 0 | 2899.48 | 344.84 | 157.57 | 703 | 92.78 | 423.884 |
|  Transformation | 4G | 1000 | 50 | 30 | 0 | 2864.18 | 348.93 | 157.15 | 707 | 92.49 | 435.324 |
|  Transformation | 4G | 1000 | 50 | 500 | 0 | 1858.21 | 537.98 | 67.78 | 699 | 95.53 | 313.886 |
|  Transformation | 4G | 1000 | 50 | 1000 | 0 | 980.82 | 1017.62 | 30.36 | 1167 | 96.27 | 72.37 |
|  Transformation | 4G | 1000 | 1024 | 0 | 0 | 2282.56 | 438.04 | 178.8 | 871 | 93.6 | 368.029 |
|  Transformation | 4G | 1000 | 1024 | 30 | 0 | 2301.88 | 434.13 | 170.69 | 843 | 93.64 | 370.068 |
|  Transformation | 4G | 1000 | 1024 | 500 | 0 | 1604.64 | 622.69 | 117.05 | 883 | 95.45 | 306.869 |
|  Transformation | 4G | 1000 | 1024 | 1000 | 0 | 957.64 | 1042.52 | 49.44 | 1239 | 95.44 | 72.046 |
|  Transformation | 4G | 1000 | 10240 | 0 | 0 | 697.56 | 1431.44 | 307.33 | 2255 | 95.52 | 262.065 |
|  Transformation | 4G | 1000 | 10240 | 30 | 0 | 700.73 | 1424.89 | 274.05 | 2175 | 95.16 | 229.717 |
|  Transformation | 4G | 1000 | 10240 | 500 | 0 | 656.79 | 1520.55 | 345.53 | 2495 | 94.33 | 363.805 |
|  Transformation | 4G | 1000 | 10240 | 1000 | 0 | 529.84 | 1882.35 | 374.94 | 2735 | 95.42 | 292.704 |
