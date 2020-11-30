# Instrumenting with Honeycomb.io

This explains an initial attempt of instrumenting with Honeycomb.io.

Here are the steps done to try it over our current architecture:

1. Install `honeycomb-beeline` npm module,
1. Add dependency in `server-remote.js`
    ```shell
    const beeline = require('honeycomb-beeline')({
      writeKey: '***',
      dataset: 'sre-project',
      serviceName: 'counter'
    });
    ```
1. Add some traces in the `server-remote.js` HTTP handler, e.g.
    ```shell
    let trace = beeline.startTrace({request: 'started'});
    //...
    beeline.finishTrace(trace);
    ```
1. Run the server in one shell,
1. Perform some requests in different CPU conditions.

The POC succeeded and some logs where recorded in Honeycomb.io board; see some screenshots below:

![](./honeycomb/one.png)
![](./honeycomb/two.png)
![](./honeycomb/three.png)
![](./honeycomb/four.png)