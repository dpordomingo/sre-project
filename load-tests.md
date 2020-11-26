# Pruebas de carga

Hacemos pruebas de carga contra distintas configuraciones de arquitectura

## Prueba de carga contra un servidor independiente funcionando con un redis local

### autocannon
`autocannon -d 10 -c 100 -p 10 http://35.181.48.132:7017/turno/local`
```
Running 10s test @ http://35.181.48.132:7017/turno/local
100 connections with 10 pipelining factor

┌─────────┬──────┬──────┬───────┬───────┬─────────┬──────────┬────────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev    │ Max    │
├─────────┼──────┼──────┼───────┼───────┼─────────┼──────────┼────────┤
│ Latency │ 0 ms │ 3 ms │ 73 ms │ 85 ms │ 9.96 ms │ 20.36 ms │ 272 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴──────────┴────────┘
┌───────────┬────────┬────────┬─────────┬────────┬─────────┬─────────┬────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%     │ 97.5%  │ Avg     │ Stdev   │ Min    │
├───────────┼────────┼────────┼─────────┼────────┼─────────┼─────────┼────────┤
│ Req/Sec   │ 4001   │ 4001   │ 10503   │ 11511  │ 9843.71 │ 2123.94 │ 4000   │
├───────────┼────────┼────────┼─────────┼────────┼─────────┼─────────┼────────┤
│ Bytes/Sec │ 764 kB │ 764 kB │ 2.01 MB │ 2.2 MB │ 1.88 MB │ 406 kB  │ 764 kB │
└───────────┴────────┴────────┴─────────┴────────┴─────────┴─────────┴────────┘

Req/Bytes counts sampled once per second.

98k requests in 10.19s, 18.8 MB read
```

10000 peticiones por segundo

### wrk2
`wrk -t10 -c100 -d10s --rate 20000 http://35.181.48.132:7017/turno/local`
```
Running 10s test @ http://35.181.48.132:7017/turno/local
  10 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     3.07s     1.61s    5.78s    58.00%
    Req/Sec       -nan      -nan   0.00      0.00%
  84156 requests in 10.00s, 15.33MB read
Requests/sec:   8414.60
Transfer/sec:      1.53MB
```

8500 peticiones por segundo

### loadtest
`loadtest -c 100 -t 10 --keepalive http://35.181.48.132:7017/turno/local`
```
[Thu Nov 26 2020 18:08:52 GMT+0000 (Coordinated Universal Time)] INFO Requests: 0, requests per second: 0, mean latency: 0 ms
[Thu Nov 26 2020 18:08:57 GMT+0000 (Coordinated Universal Time)] INFO Requests: 26805, requests per second: 5378, mean latency: 18.7 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Target URL:          http://35.181.48.132:7017/turno/local
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Max time (s):        10
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Concurrency level:   100
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Agent:               keepalive
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Completed requests:  58617
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Total errors:        0
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Total time:          10.00181484 s
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Requests per second: 5861
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Mean latency:        17 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO Percentage of the requests served within a certain time
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO   50%      14 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO   90%      19 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO   95%      27 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO   99%      49 ms
[Thu Nov 26 2020 18:09:02 GMT+0000 (Coordinated Universal Time)] INFO  100%      112 ms (longest request)
```

5800 peticiones por segundo

## Prueba de carga contra un servidor independiente funcionando con un servicio redis de AWS

### autocannon
`autocannon -d 10 -c 100 -p 10 http://35.181.48.132:7017/turno/memory`
```
Running 10s test @ http://35.181.48.132:7017/turno/memory
100 connections with 10 pipelining factor

┌─────────┬──────┬──────┬───────┬───────┬─────────┬─────────┬────────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev   │ Max    │
├─────────┼──────┼──────┼───────┼───────┼─────────┼─────────┼────────┤
│ Latency │ 0 ms │ 0 ms │ 20 ms │ 25 ms │ 3.74 ms │ 9.23 ms │ 236 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴─────────┴────────┘
┌───────────┬────────┬────────┬─────────┬─────────┬──────────┬─────────┬─────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%     │ 97.5%   │ Avg      │ Stdev   │ Min     │
├───────────┼────────┼────────┼─────────┼─────────┼──────────┼─────────┼─────────┤
│ Req/Sec   │ 14175  │ 14175  │ 27007   │ 27855   │ 25801.82 │ 3724.48 │ 14168   │
├───────────┼────────┼────────┼─────────┼─────────┼──────────┼─────────┼─────────┤
│ Bytes/Sec │ 2.7 MB │ 2.7 MB │ 5.18 MB │ 5.35 MB │ 4.94 MB  │ 721 kB  │ 2.69 MB │
└───────────┴────────┴────────┴─────────┴─────────┴──────────┴─────────┴─────────┘

Req/Bytes counts sampled once per second.

284k requests in 11.18s, 54.4 MB read
```

26000 peticiones por segundo

### wrk2
`wrk -t10 -c100 -d10s --rate 20000 http://35.181.48.132:7017/turno/memory`
```
Running 10s test @ http://35.181.48.132:7017/turno/memory
  10 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.10s     1.03s    4.47s    59.01%
    Req/Sec       -nan      -nan   0.00      0.00%
  123559 requests in 10.00s, 22.62MB read
Requests/sec:  12357.35
Transfer/sec:      2.26MB
```

7500 peticiones por segundo

### loadtest
`loadtest -c 100 -t 10 --keepalive http://35.181.48.132:7017/turno/memory`
```
[Thu Nov 26 2020 18:11:37 GMT+0000 (Coordinated Universal Time)] INFO Requests: 0, requests per second: 0, mean latency: 0 ms
[Thu Nov 26 2020 18:11:42 GMT+0000 (Coordinated Universal Time)] INFO Requests: 26182, requests per second: 5245, mean latency: 19.2 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Target URL:          http://35.181.48.132:7017/turno/memory
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Max time (s):        10
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Concurrency level:   100
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Agent:               keepalive
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Completed requests:  57420
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Total errors:        0
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Total time:          10.000420803 s
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Requests per second: 5742
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Mean latency:        17.3 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Percentage of the requests served within a certain time
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO   50%      15 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO   90%      19 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO   95%      27 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO   99%      50 ms
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO  100%      85 ms (longest request)
[Thu Nov 26 2020 18:11:47 GMT+0000 (Coordinated Universal Time)] INFO Requests: 57420, requests per second: 6264, mean latency: 15.8 ms
```

5800 peticiones por segundo

## Prueba de carga contra un servidor independiente funcionando con un servicio redis remoto

### autocannon
`autocannon -d 10 -c 100 -p 10 http://35.181.48.132:7017/turno/remote`
```
Running 10s test @ http://35.181.48.132:7017/turno/remote
100 connections with 10 pipelining factor

┌─────────┬──────┬──────┬───────┬───────┬─────────┬──────────┬────────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev    │ Max    │
├─────────┼──────┼──────┼───────┼───────┼─────────┼──────────┼────────┤
│ Latency │ 0 ms │ 0 ms │ 33 ms │ 40 ms │ 5.16 ms │ 10.48 ms │ 260 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴──────────┴────────┘
┌───────────┬────────┬────────┬─────────┬────────┬─────────┬─────────┬─────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%     │ 97.5%  │ Avg     │ Stdev   │ Min     │
├───────────┼────────┼────────┼─────────┼────────┼─────────┼─────────┼─────────┤
│ Req/Sec   │ 6295   │ 6295   │ 19615   │ 21871  │ 18598.2 │ 4246.26 │ 6295    │
├───────────┼────────┼────────┼─────────┼────────┼─────────┼─────────┼─────────┤
│ Bytes/Sec │ 1.2 MB │ 1.2 MB │ 3.75 MB │ 4.2 MB │ 3.56 MB │ 818 kB  │ 1.19 MB │
└───────────┴────────┴────────┴─────────┴────────┴─────────┴─────────┴─────────┘

Req/Bytes counts sampled once per second.

186k requests in 10.19s, 35.6 MB read
```

18500 peticiones por segundo

### wrk2
`wrk -t10 -c100 -d10s --rate 20000 http://35.181.48.132:7017/turno/remote`
```
Running 10s test @ http://35.181.48.132:7017/turno/remote
  10 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.86s   927.89ms   3.49s    58.23%
    Req/Sec       -nan      -nan   0.00      0.00%
  129007 requests in 10.00s, 23.62MB read
Requests/sec:  12900.84
Transfer/sec:      2.36MB
```

12900 peticiones por segundo

### loadtest
`loadtest -c 100 -t 10 --keepalive http://35.181.48.132:7017/turno/remote`
```
[Thu Nov 26 2020 18:39:08 GMT+0000 (Coordinated Universal Time)] INFO Requests: 0, requests per second: 0, mean latency: 0 ms
[Thu Nov 26 2020 18:39:13 GMT+0000 (Coordinated Universal Time)] INFO Requests: 26862, requests per second: 5382, mean latency: 18.7 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Target URL:          http://35.181.48.132:7017/turno/remote
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Max time (s):        10
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Concurrency level:   100
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Agent:               keepalive
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Completed requests:  59672
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Total errors:        0
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Total time:          10.000404019 s
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Requests per second: 5967
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Mean latency:        16.7 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Percentage of the requests served within a certain time
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO   50%      14 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO   90%      17 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO   95%      27 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO   99%      50 ms
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO  100%      85 ms (longest request)
[Thu Nov 26 2020 18:39:18 GMT+0000 (Coordinated Universal Time)] INFO Requests: 59672, requests per second: 6578, mean latency: 15 ms
```

6000 peticiones por segundo

## Balanceador con una instancia

`autocannon -d 10 -c 100 -p 10 http://turnomatic-balance-1545372966.eu-west-3.elb.amazonaws.com/turno/balance-one-instance`
```
Running 10s test @ http://turnomatic-balance-1545372966.eu-west-3.elb.amazonaws.com/turno/balance-one-instance
100 connections with 10 pipelining factor

┌─────────┬──────┬──────┬───────┬───────┬─────────┬─────────┬────────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev   │ Max    │
├─────────┼──────┼──────┼───────┼───────┼─────────┼─────────┼────────┤
│ Latency │ 4 ms │ 8 ms │ 14 ms │ 21 ms │ 8.42 ms │ 5.82 ms │ 211 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴─────────┴────────┘
┌───────────┬─────────┬─────────┬─────────┬─────────┬──────────┬─────────┬─────────┐
│ Stat      │ 1%      │ 2.5%    │ 50%     │ 97.5%   │ Avg      │ Stdev   │ Min     │
├───────────┼─────────┼─────────┼─────────┼─────────┼──────────┼─────────┼─────────┤
│ Req/Sec   │ 7887    │ 7887    │ 11695   │ 11919   │ 11262.37 │ 1102.84 │ 7885    │
├───────────┼─────────┼─────────┼─────────┼─────────┼──────────┼─────────┼─────────┤
│ Bytes/Sec │ 1.43 MB │ 1.43 MB │ 2.13 MB │ 2.17 MB │ 2.05 MB  │ 204 kB  │ 1.43 MB │
└───────────┴─────────┴─────────┴─────────┴─────────┴──────────┴─────────┴─────────┘

Req/Bytes counts sampled once per second.

124k requests in 11.16s, 22.6 MB read
```

11200 peticiones por segundo

## Balanceador con dos instancia

`autocannon -d 10 -c 100 -p 10 http://turnomatic-balance-1545372966.eu-west-3.elb.amazonaws.com/turno/balance-two-instances`
```
Running 10s test @ http://turnomatic-balance-1545372966.eu-west-3.elb.amazonaws.com/turno/balance-two-instances
100 connections with 10 pipelining factor

┌─────────┬──────┬──────┬───────┬───────┬─────────┬─────────┬────────┐
│ Stat    │ 2.5% │ 50%  │ 97.5% │ 99%   │ Avg     │ Stdev   │ Max    │
├─────────┼──────┼──────┼───────┼───────┼─────────┼─────────┼────────┤
│ Latency │ 0 ms │ 6 ms │ 12 ms │ 16 ms │ 6.31 ms │ 6.92 ms │ 339 ms │
└─────────┴──────┴──────┴───────┴───────┴─────────┴─────────┴────────┘
┌───────────┬─────────┬─────────┬─────────┬─────────┬─────────┬─────────┬─────────┐
│ Stat      │ 1%      │ 2.5%    │ 50%     │ 97.5%   │ Avg     │ Stdev   │ Min     │
├───────────┼─────────┼─────────┼─────────┼─────────┼─────────┼─────────┼─────────┤
│ Req/Sec   │ 10279   │ 10279   │ 14935   │ 16703   │ 14802   │ 1598.85 │ 10278   │
├───────────┼─────────┼─────────┼─────────┼─────────┼─────────┼─────────┼─────────┤
│ Bytes/Sec │ 1.89 MB │ 1.89 MB │ 2.75 MB │ 3.07 MB │ 2.72 MB │ 294 kB  │ 1.89 MB │
└───────────┴─────────┴─────────┴─────────┴─────────┴─────────┴─────────┴─────────┘

Req/Bytes counts sampled once per second.

148k requests in 10.15s, 27.2 MB read
```

14000 peticiones por segundo

## Balanceador con tres instancias

Hemos probado con tres instancias y los resultados son prácticamente idénticos a la configuración con dos instancias. Todo apunta a que es el balanceador de carga.

## Balanceo por DNS

Hacemos una prueba simulada de un balance por DNS con una prueba de carga simultánea a cada uno de los tres servidores. Obtenemos unas 18.5k peticiones por segundo en cada servidor, en total 55.5k peticiones por segundo. Con este tipo de balanceo conseguimos aumentar linealmente el número de peticiones por segundo aumentando la cantidad de servidores.

# Resumen de resultados de las peticiones por segundo

|                          | autocannon | wrk2  | loadtest |
|--------------------------|------------|-------|----------|
| standalone redis local   |      10000 |  8500 |     5800 |
| standalone redis AWS     |      26000 |  7500 |     5800 |
| standalone redis remote  |      18500 | 12900 |     6000 |
| balanceador 1 instancia  |      11200 |       |          |
| balanceador 2 instancias |      14000 |       |          |
| balanceador 3 instancias |      14000 |       |          |
| balanceador DNS 2 inst   |      37000 |       |          |
| balanceador DNS 3 inst   |      55500 |       |          |

# Conclusiones

Nos encontramos con un límite en el balanceador de carga de AWS, parece ser que tiene un límite de unas 14000 peticiones por segundo. Es posible que Amazon pueda incrementar ese límite pero no sabemos hasta dónde podríamos llegar.

Con balanceo por DNS podríamos escalar el número de peticiones por segundo de manera lineal respecto al número de servidores.
