# Core-micro-services Logging

Module Includes Brainstrom-auth docker image, Elastic Search and Kibana running as host network


### Node js example


```
const winston = require('winston');
const Elasticsearch = require('winston-elasticsearch');

const esTransportOpts1 = {
  level: 'info',
  indexPrefix: 'info'
};

const esTransportOpts2 = {
  level: 'error',
  indexPrefix: 'error'
};
export const infoLogger = winston.createLogger({
  transports: [
    new Elasticsearch(esTransportOpts1)
  ]
});
export const errorLogger = winston.createLogger({
  transports: [
    new Elasticsearch(esTransportOpts2)
  ]
});
```


```
import { infoLogger } from '../winston-elastic';

...

      infoLogger.info('Info', {
        status: ctx.status,
        profile: profile._id,
        body: JSON.stringify(ctx.request.body),
        method: ctx.req.method,
        url: ctx.req.url,
        resp: JSON.stringify(record)
      });
```
