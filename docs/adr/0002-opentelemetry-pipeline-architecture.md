# ADR 0002: Standardizing on the OpenTelemetry Architecture

## Status
Accepted

## Context
A major failure mode of legacy platform architectures is vendor lock-in caused by scattering proprietary monitoring agents (e.g., Datadog, New Relic) across infrastructure and codebases. To ensure long-term platform flexibility and unified telemetry processing, the platform control plane requires a standard, vendor-agnostic ingestion layer.

## Decision
We explicitly standardize on the OpenTelemetry (OTel) standard for all metric, trace, and log collections across the platform.
1. **Application Layer:** Leverage the OpenTelemetry Kubernetes Operator to enforce zero-touch Auto-Instrumentation at runtime for developer workloads.
2. **Collector Layer:** Deploy a centralized OpenTelemetry Collector architecture inside the secure `/observability` namespace.
3. **Decoupled Backends:** The platform pipeline will handle all processing and attributes routing locally before securely forwarding data to interchangeable backend visualization layers.

## Consequences
* **Positive:** Absolute protection against telemetry vendor lock-in.
* **Positive:** Drastic reduction in cloud egress costs by filtering and sampling traces at the cluster boundary before export.
* **Negative:** Higher Day-1 platform management overhead to maintain the OTel Operator lifecycle.

