# `thoughtspot-re-data-generator`

Thoughtspot Real Estate data generator

## Overview

NodeJS command utility that will generate data intended to be consumed by the Thoughtspot Search applicance.
The data flow intended for this utility:

Elasticsearch source data > utility > Elasticsearch generated Thoughtspot data > estab > CSV flat files > Thoughtspot

> Yes, this is a lot of steps...
