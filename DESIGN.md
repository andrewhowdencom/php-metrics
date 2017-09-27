# Design Document

## Motivation / Requirement

Time series data exposed by an application can provide extremely rapid feedback on an applications performance. This
information can be used for a number of useful processes such as:

- Allowing infrastructure to make decisions around whether to modify the applications runtime environment<sup>[k8s-hpa](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)</sup>
- Debugging the application performance during runtime<sup>[prom-instrumentation](https://prometheus.io/docs/practices/instrumentation/)</sup>
- Alerting when an application violates it's SLO<sup>[sre-slo](https://landing.google.com/sre/book/chapters/service-level-objectives.html)</sup>

## APIs

- We need:
  - Some sort of registry object that functions as a storage abstraction for all metrics.
  - Classes for each metric type, as well as to have them constructed in some way, and persisted.
  - Documented ways to persist metrics to the registry
  - Documented ways to query all metrics from registry (a collection? a simple array of objects? unsure)

Outstanding questions:

- Do we want to support lazy construction? I.e. just being able to persist metrics within application, and lazily handle stuff.
- Are the Prometheus abstractions (gauge, count, histogram and summary) suitable?
- How do we append time metadata to metrics that support it? or do we?

## Non Goals

### Provide specific recommendations about how to instrument applications

The goal of this work is rather to provide or adopt a common language that can be used to describe application state.
Specific recommendations about how to instrument applications is a related issue, but not one that is the concern
of this project.

## Related Reading

- http://www.brendangregg.com/usemethod.html
- https://prometheus.io/docs/introduction/overview/
- https://github.com/DataDog/php-datadogstatsd
- https://github.com/Jimdo/prometheus_client_php
