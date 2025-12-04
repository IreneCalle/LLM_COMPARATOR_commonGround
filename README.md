# 🧪 LLM Evaluation Suite

**Two complementary tools for comprehensive LLM evaluation**

| Tool | Purpose | Approach |
|------|---------|----------|
| 🤝 **commonGround** | Qualitative analysis | Consensus, coherence, LLM-as-judge |
| 📊 **commonBench** | Quantitative benchmarking | Latency, cost, error rate, TTFT |

People often ask me which LLM they should use. These tools help you answer that question with data—both qualitative consensus and quantitative metrics.

---

## 🤝 commonGround - Consensus Analyzer

Compare responses from multiple LLMs, find what they agree on, and let Claude judge the winner.

### What it does

- **Query 4 LLMs** simultaneously with the same question
- **Find consensus** - the 3 main points all models agree on
- **Measure coherence** - how well responses align (1-10)
- **Assess quality** - detect hallucinations, off-topic responses, subjectivity
- **Get a verdict** - Claude judges the winner based on your objective

### Quality Metrics (Qualitative)

| Metric | What it measures |
|--------|------------------|
| **Hallucination** | Does it contain false information? |
| **Imprecise** | Is it vague or lacking detail? |
| **Off-Topic** | Does it stray from the question? |
| **Subjective** | Is it overly opinionated? |
| **Overly Enthusiastic** | Does it exaggerate? |
| **Coherence Score** | How well does it align with other responses? (1-10) |

### Best for
- Evaluating prompt effectiveness
- Understanding model biases
- Finding the most reliable model for specific tasks
- Research on LLM behavior

---

## 📊 commonBench - Technical Benchmarking

Measure quantitative performance metrics across multiple models and iterations.

### What it does

- **Benchmark multiple LLMs** with configurable iterations (1-30)
- **Measure real costs** - dynamic pricing from OpenRouter API
- **Capture TTFT** - Time to First Token (critical UX metric)
- **Track reliability** - error rate as operational quality metric
- **Estimate costs** - before running expensive benchmarks

### Performance Metrics (Quantitative)

#### Tier 1: Speed & Tokens
| Metric | What it measures | Good is... |
|--------|------------------|------------|
| `latency_sec` | Total response time | Low |
| `ttft_sec` | Time to First Token | Low (<1s) |
| `tokens_per_sec` | Generation throughput | High |
| `input_tokens` | Tokens sent | - |
| `output_tokens` | Tokens received | - |

#### Tier 2: Cost
| Metric | What it measures | Good is... |
|--------|------------------|------------|
| `cost_usd` | Actual cost per call | Low |
| `is_free` | Whether model is free tier | - |
| `pricing_source` | Where price came from (api/fallback) | api |

#### Tier 3: Text Quality
| Metric | What it measures | Good is... |
|--------|------------------|------------|
| `lexical_diversity` | Unique words / total words | 0.6-0.8 |
| `readability_flesch` | Flesch Reading Ease score | 60-70 |
| `word_count` | Response length | Depends on task |

#### Tier 4: Operational Quality
| Metric | What it measures | Good is... |
|--------|------------------|------------|
| `error_rate_%` | Percentage of failed calls | Low (<5%) |
| `availability_%` | Percentage of successful calls | High (>95%) |
| `retry_count` | Retries needed | Low (0) |

#### Tier 5: Optional
| Metric | What it measures | Good is... |
|--------|------------------|------------|
| `f1_score` | Word overlap with reference | High |

### Best for
- Model selection for production
- Cost optimization
- Detecting performance regressions
- Comparing price/performance tradeoffs

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Jupyter Notebook
- OpenRouter API key ([Get one here](https://openrouter.ai/keys))

### Installation

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd llm-evaluation-suite

# 2. Create environment file
cp .env.example .env

# 3. Add your API key to .env
OPENROUTER_API_KEY=your_key_here

# 4. Open the notebook you want
jupyter notebook commonGround.ipynb  # Port 7867
# or
jupyter notebook commonBench_v2.ipynb  # Port 7868
```

Both tools can run simultaneously on different ports.

---

## 🔄 When to Use Each Tool

| Scenario | Use |
|----------|-----|
| "Which model gives the best answer?" | 🤝 commonGround |
| "Which model is fastest and cheapest?" | 📊 commonBench |
| "Do models agree on this topic?" | 🤝 commonGround |
| "How consistent is this model?" | 📊 commonBench (multiple iterations) |
| "Is this model hallucinating?" | 🤝 commonGround |
| "What's the real cost of using this model?" | 📊 commonBench |
| "Which model has best UX (fast first response)?" | 📊 commonBench (TTFT) |
| "Which model best meets my specific objective?" | 🤝 commonGround |

### Using Both Together

1. **Start with commonBench** to narrow down candidates based on cost/speed
2. **Then use commonGround** to evaluate quality among the finalists

---

## 🌐 About OpenRouter

[OpenRouter](https://openrouter.ai) provides unified access to 100+ LLMs through a single API:

- ✅ Single API key for all providers
- ✅ Pay-as-you-go pricing
- ✅ Many free models available (marked with `:free`)
- ✅ OpenAI-compatible interface

---

## 📁 Project Structure

```
llm-evaluation-suite/
├── commonGround.ipynb     # Qualitative consensus analyzer
├── commonBench_v2.ipynb   # Quantitative benchmarking tool
├── .env.example           # Environment template
├── .env                   # Your API key (not committed)
└── README.md              # This file
```

---

## 🛠️ Technical Details

### commonGround Architecture
```
User Input → 4 Parallel LLM Calls → Consensus Analysis (Claude)
                                  → Quality Metrics Extraction
                                  → Final Verdict (Claude)
```

### commonBench Architecture
```
User Input → Cost Estimation → N×M LLM Calls (with retry)
                             → Metrics Collection (TTFT, latency, cost)
                             → Error Rate Tracking
                             → Aggregated Statistics
```

### Key Technical Features

| Feature | commonGround | commonBench |
|---------|--------------|-------------|
| Parallel calls | ✅ | ✅ |
| Error handling | Basic | Advanced (retry + backoff) |
| Cost tracking | ❌ | ✅ Dynamic pricing |
| TTFT measurement | ❌ | ✅ Via streaming |
| Multiple iterations | ❌ | ✅ 1-30 |
| LLM-as-judge | ✅ Claude | ❌ |
| Export results | ❌ | ✅ CSV |

---

## 💡 Tips

### For commonGround
- Be specific with your question
- Define clear objectives for the judge
- Mix different model sizes and providers

### For commonBench
- Use 5-10 iterations for reliable statistics
- Check `std` (standard deviation) for consistency
- Compare `error_rate` alongside raw performance
- Look at TTFT for user-facing applications

---

## 📊 Understanding the Metrics

### Why TTFT matters
Time to First Token measures when the user sees the first character. A model with 0.3s TTFT feels faster than one with 2s TTFT, even if total latency is similar.

### Why error_rate matters
A model with 95% accuracy but 20% error rate has worse *operational quality* than one with 90% accuracy and 2% error rate. Reliability is a quality metric.

### Why dynamic pricing matters
LLM prices change frequently. Hardcoded prices become wrong within weeks. commonBench fetches current prices from OpenRouter's API.

---

## 🤝 Contributing

Feel free to:
- Add more models to the available lists
- Improve analysis prompts
- Add new metrics
- Enhance visualizations

---

## 📄 License

Open-source for educational and research purposes.

---

**Ready to evaluate?** Start with the tool that matches your question:
- *"Which response is best?"* → 🤝 commonGround
- *"Which model performs best?"* → 📊 commonBench
