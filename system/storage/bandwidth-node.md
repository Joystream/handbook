---
description: >-
  Bandwidth nodes deliver data objects on-demand to end users at low latency by
  caching data objects and replicating them from storage providers upon cache
  misses.
---

# Bandwidth Node

## Preamble

This document is not yet complete and is primarily informed by the following more comprehensive documentation

{% embed url="https://github.com/Joystream/joystream/tree/giza_staging/distributor-node" %}

## Introduction

WIP.

## API

### status

{% swagger src="https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml" path="/status" method="get" %}
[https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml](https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml)
{% endswagger %}

### buckets

{% swagger src="https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml" path="/buckets" method="get" %}
[https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml](https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml)
{% endswagger %}

### asset

#### GET

{% swagger src="https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml" path="/asset/{objectId}" method="get" %}
[https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml](https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml)
{% endswagger %}

#### HEAD

{% swagger src="https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml" path="/asset/{objectId}" method="head" %}
[https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml](https://raw.githubusercontent.com/Joystream/joystream/giza_staging/distributor-node/src/api-spec/openapi.yml)
{% endswagger %}

## Scenarios

WIP.
