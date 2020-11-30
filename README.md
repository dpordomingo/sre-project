# sre-project

Final project for [SRE: Escalabilidad en entornos de alto rendimiento](https://trainingit.es/curso-sre-escalabilidad/) course. (see [specs](https://github.com/SRETriT/curso-escalabilidad-v2/blob/main/sesion-6/cdev2-6-proyecto.pdf))

## Problem to solve

Service exposing an endpoint offering consecutive counter for a given id.

```bash
$ curl http://localhost:7017/turno/given_id
{
  id: "given_id",
  turno: 33
}
```

It must accept and serve at least 100k RPS, and should be capable to attend 200k RPS with no major architectural changes.

## Index

- [Description of the architecture](architecture.md)
- [Load tests](load-tests.md)
- [Balancing](balancing.md)
- [Monitoring](monitoring.md)
  - [Instrumenting with honeycomb.io](./docs/monitoring/honeycomb.md)
- [Scalability report](scalability-report.md)
- Incidents
  - [Framework to deal with incidents](./docs/incidents/README.md)
  - [Inventory of past incidents](./docs/incidents/history/)

## Authors

- Ángel ([senechaux](https://github.com/senechaux))
- David ([dpordomingo](https://github.com/dpordomingo))

## License

MIT License, see [LICENSE](./LICENSE.md).
