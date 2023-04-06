
## Observability Stack

Posthog, Sentry, OpenReplay, LGTM stack, OpenTelemetry, SigNoz

OpenTelemetry has become acknowledged as the open standard for instrumentation. The spec includes metrics, logs, and traces.

Summarizing the differences between the software:

- Open source
    - Sentry, OpenReplay, Posthog
- SigNoz integrates traces, logs and metrics

Grafana has been adopting OpenTelemetry with its new products like Grafana Mimir, Grafana Tempo, etc.

For code instrumentation, I would choose to use otel instrumentation libs and signoz as a backend. Then for client observability features like session replay and performance monitoring I would use open replay. It already has integrations with sentry’s distributed tracing. Maybe an OpenTelemetry integration will be developed later.

Sentry’s OpenTelemetry integration is under development.

Posthog is client-focused, even though it supports tracing events all over the stack with clients for multiple languages. However, you have to craft custom events grouped into actions across multiple services. I can see this getting overwhelming pretty soon into development of multiple services.