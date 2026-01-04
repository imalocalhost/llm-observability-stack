# LLM Observability Stack

> Production-grade monitoring, tracing, and analytics for LLM applications

[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)](https://grafana.com/)
[![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)](https://prometheus.io/)
[![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?logo=opentelemetry&logoColor=white)](https://opentelemetry.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🎯 Problem Statement

Production LLM applications lack critical observability:

- **No visibility** - Can't see what happens inside LLM calls
- **No debugging** - When responses fail, no trace of why
- **No cost tracking** - Spend money without knowing where
- **No latency monitoring** - Can't identify performance bottlenecks
- **No quality metrics** - Don't know if outputs are good
- **No alerting** - Issues discovered by users, not monitoring

**Result:** Blind operations, budget overruns, poor user experience.

## 💡 Solution

A complete observability stack for LLM applications:

✅ **Distributed tracing** - Track requests across services  
✅ **Metrics collection** - Cost, latency, tokens, success rate  
✅ **Logging** - Capture all LLM inputs/outputs  
✅ **Dashboards** - Visualize system health in real-time  
✅ **Alerting** - Get notified before users complain  
✅ **Cost analytics** - Attribution and budget tracking  

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│             Your LLM Application                    │
│  ┌──────────────────────────────────────────────┐   │
│  │  Instrumented with OpenTelemetry SDK        │   │
│  │  - Traces: Function calls, LLM requests     │   │
│  │  - Metrics: Cost, latency, tokens           │   │
│  │  - Logs: Prompts, responses, errors         │   │
│  └────────┬────────────────────────────────────┘   │
└───────────┼─────────────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────────────────┐
│     OpenTelemetry Collector (OTLP)                  │
│  ┌──────────────────────────────────────────────┐   │
│  │  Receive, Process, Export                    │   │
│  │  - Sampling                                   │   │
│  │  - Filtering                                  │   │
│  │  - Enrichment                                │   │
│  └──────┬────────────────┬──────────────────────┘   │
└─────────┼────────────────┼─────────────────────────┘
          │                │
     ┌────▼────┐      ┌───▼───┐
     │  Tempo  │      │ Loki  │ (Traces & Logs)
     │(Traces) │      │(Logs) │
     └────┬────┘      └───┬───┘
          │               │
          └───────┬───────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────┐
│              Grafana Dashboards                     │
│  ┌──────────────────────────────────────────────┐   │
│  │  - LLM Performance Dashboard                 │   │
│  │  - Cost Analytics Dashboard                  │   │
│  │  - Error Rate Dashboard                      │   │
│  │  - Trace Explorer                            │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────┐
│      Alertmanager (Prometheus)                      │
│  ┌──────────────────────────────────────────────┐   │
│  │  Alerts: Cost spikes, latency, errors        │   │
│  │  Channels: Slack, PagerDuty, Email          │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

## 🚀 Features

### Distributed Tracing
- **Full request tracing** - See entire request flow
- **LLM call visibility** - Prompt, response, latency per call
- **Span relationships** - Parent-child traces across services
- **Error tracking** - Failed requests with context
- **Performance profiling** - Identify bottlenecks

### Metrics & Analytics
- **Cost tracking**:
  - Total spend per day/week/month
  - Cost per endpoint/user/tenant
  - Model comparison (GPT-4 vs Claude)
- **Latency monitoring**:
  - p50, p95, p99 percentiles
  - Time to first token (TTFT)
  - Total request duration
- **Token usage**:
  - Input/output tokens per request
  - Token rate trends
  - Cost per 1k tokens
- **Quality metrics**:
  - Success rate
  - Retry rate
  - User feedback scores

### Logging
- **Structured logging** - JSON format for easy parsing
- **Prompt/response capture** - Full LLM I/O logged
- **PII redaction** - Automatic sensitive data masking
- **Log aggregation** - Centralized search across services
- **Retention policies** - Configurable storage duration

### Dashboards
Pre-built Grafana dashboards:
- **LLM Performance** - Latency, throughput, errors
- **Cost Analytics** - Spending trends, attribution
- **Model Comparison** - Performance across providers
- **User Analytics** - Usage patterns per user/tenant
- **Alert Overview** - Active alerts and trends

### Alerting
- **Cost alerts** - Budget thresholds exceeded
- **Latency alerts** - p95 above threshold
- **Error rate alerts** - Failures spike
- **Token usage alerts** - Unusual consumption
- **Custom alerts** - Define your own rules

## 🛠️ Tech Stack

**Instrumentation:**
- OpenTelemetry SDK (TypeScript/Python)
- Auto-instrumentation libraries

**Collection & Storage:**
- OpenTelemetry Collector - Data pipeline
- Grafana Tempo - Distributed tracing
- Grafana Loki - Log aggregation
- Prometheus - Metrics & alerting

**Visualization:**
- Grafana - Dashboards & visualization
- Alertmanager - Alert routing

**Infrastructure:**
- Docker Compose - Local development
- Kubernetes - Production deployment (optional)

## 📦 Installation

### Prerequisites
- Docker & Docker Compose
- Your LLM application (TypeScript or Python)

### Quick Start

```bash
# Clone repository
git clone https://github.com/imalocalhost/llm-observability-stack.git
cd llm-observability-stack

# Start the stack
docker-compose up -d

# Verify services
docker-compose ps
```

**Access:**
- Grafana: `http://localhost:3000` (admin/admin)
- Prometheus: `http://localhost:9090`
- Jaeger UI: `http://localhost:16686`

## 🔌 Instrument Your Application

### TypeScript/Node.js

```typescript
// Install dependencies
npm install @opentelemetry/sdk-node \
            @opentelemetry/auto-instrumentations-node \
            @opentelemetry/exporter-trace-otlp-http

// instrumentation.ts
import { NodeSDK } from '@opentelemetry/sdk-node';
import { getNodeAutoInstrumentations } from '@opentelemetry/auto-instrumentations-node';
import { OTLPTraceExporter } from '@opentelemetry/exporter-trace-otlp-http';

const sdk = new NodeSDK({
  traceExporter: new OTLPTraceExporter({
    url: 'http://localhost:4318/v1/traces',
  }),
  instrumentations: [getNodeAutoInstrumentations()],
  serviceName: 'my-llm-app',
});

sdk.start();

// app.ts
import './instrumentation';
import { trace } from '@opentelemetry/api';

const tracer = trace.getTracer('llm-calls');

async function callLLM(prompt: string) {
  const span = tracer.startSpan('llm.call', {
    attributes: {
      'llm.provider': 'openai',
      'llm.model': 'gpt-4',
      'llm.prompt': prompt,
    },
  });

  try {
    const response = await openai.chat.completions.create({
      model: 'gpt-4',
      messages: [{ role: 'user', content: prompt }],
    });

    span.setAttributes({
      'llm.response': response.choices[0].message.content,
      'llm.tokens.input': response.usage.prompt_tokens,
      'llm.tokens.output': response.usage.completion_tokens,
      'llm.cost': calculateCost(response.usage),
    });

    return response;
  } catch (error) {
    span.recordException(error);
    throw error;
  } finally {
    span.end();
  }
}
```

### Python

```python
# Install dependencies
pip install opentelemetry-api \
            opentelemetry-sdk \
            opentelemetry-exporter-otlp

# instrumentation.py
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter

provider = TracerProvider()
processor = BatchSpanProcessor(
    OTLPSpanExporter(endpoint="http://localhost:4318/v1/traces")
)
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)

# app.py
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

def call_llm(prompt: str):
    with tracer.start_as_current_span(
        "llm.call",
        attributes={
            "llm.provider": "anthropic",
            "llm.model": "claude-3-opus",
            "llm.prompt": prompt,
        }
    ) as span:
        response = anthropic.messages.create(
            model="claude-3-opus-20240229",
            messages=[{"role": "user", "content": prompt}]
        )
        
        span.set_attributes({
            "llm.response": response.content[0].text,
            "llm.tokens.input": response.usage.input_tokens,
            "llm.tokens.output": response.usage.output_tokens,
            "llm.cost": calculate_cost(response.usage),
        })
        
        return response
```

## 📊 Pre-Built Dashboards

### 1. LLM Performance Dashboard
- Requests per second
- Average latency (p50, p95, p99)
- Error rate
- Token usage trends
- Active LLM calls (real-time)

### 2. Cost Analytics Dashboard
- Total spend (today/week/month)
- Cost per model
- Cost per endpoint
- Cost trend over time
- Budget alerts

### 3. Model Comparison Dashboard
- Latency comparison (GPT-4 vs Claude vs Gemini)
- Cost comparison
- Success rate comparison
- Token efficiency

### 4. User Analytics Dashboard
- Requests per user
- Cost per user
- Average response time per user
- Top users by volume

### 5. Error Tracking Dashboard
- Error rate over time
- Error types breakdown
- Failed requests traces
- Retry attempts

## 🔔 Alert Rules

Pre-configured alerts:

```yaml
# High cost alert
- alert: HighLLMCost
  expr: sum(llm_cost_total) > 100
  for: 5m
  annotations:
    summary: "LLM costs exceeded $100 in 5 minutes"

# High latency alert
- alert: HighLLMLatency
  expr: histogram_quantile(0.95, llm_latency_seconds) > 5
  for: 10m
  annotations:
    summary: "p95 latency above 5 seconds"

# High error rate alert
- alert: HighErrorRate
  expr: rate(llm_errors_total[5m]) > 0.1
  for: 5m
  annotations:
    summary: "Error rate above 10%"
```

## 🧪 Testing

```bash
# Generate sample traces
npm run test:generate-traces

# Verify data in Grafana
open http://localhost:3000

# Check Prometheus metrics
open http://localhost:9090
```

## 🗺️ Roadmap

- [x] OpenTelemetry instrumentation
- [x] Grafana dashboards
- [x] Prometheus metrics
- [x] Basic alerting
- [ ] Anomaly detection (ML-based)
- [ ] Cost forecasting
- [ ] Automatic prompt optimization suggestions
- [ ] Integration with LangSmith/LangFuse
- [ ] Session replay (conversation flows)
- [ ] A/B test result tracking
- [ ] Enterprise SSO

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Add tests
4. Submit a pull request

## 📄 License

MIT License - see [LICENSE](LICENSE) file

## 🙏 Acknowledgments

- Built on OpenTelemetry standards
- Grafana Labs for amazing tools
- AI Engineering community

## 📧 Contact

**Colin** - [@imalocalhost](https://github.com/imalocalhost)

Project Link: [https://github.com/imalocalhost/llm-observability-stack](https://github.com/imalocalhost/llm-observability-stack)

---

⭐ **Star this repo if you're running LLM apps in production!**

💡 **Currently seeking remote AI Platform Engineer roles (€120K+)** - [Connect on LinkedIn](https://linkedin.com/in/yourprofile)
