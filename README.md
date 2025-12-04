# 🤝 commonGround

**Multi-Model Consensus Analyzer for LLM Evaluation**

commonGround is an interactive tool that helps you compare responses from multiple Large Language Models (LLMs) simultaneously, analyze their consensus, and identify the best-performing model based on objective criteria.
People ofter ask me which LLM they should be using on a daily basis, so I figured they might as well enjoy assess answers themselves (I DO).
## 🎯 What is commonGround?

commonGround allows you to:
- **Query 4 different LLMs** at once with the same question
- **Find consensus** - discover the 3 main points all models agree on
- **Measure coherence** - evaluate how well the responses align with each other
- **Assess quality** - automatically detect hallucinations, off-topic responses, subjectivity, and more
- **Get a verdict** - let Claude act as a judge to determine the winning model based on your objective

This is particularly useful for:
- Evaluating prompt effectiveness across different models
- Understanding LLM behavior and biases
- Finding the most reliable model for specific tasks
- Researching LLM evaluation metrics and methodologies

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab (or run it as a standalone Python script)
- I did use Cursor + UV for this.
- An OpenRouter API key ([Get one here](https://openrouter.ai/keys)) 

### Installation

1. **Clone or download** this repository

2. **Create your environment file:**
   ```bash
   cp .env.example .env
   ```

3. **Add your OpenRouter API key** to the `.env` file:
   ```
   OPENROUTER_API_KEY=your_actual_api_key_here
   ```

4. **Open the notebook:**
   ```bash
   jupyter notebook commonGround.ipynb
   ```

5. **Run all cells** - the first cell will automatically install required dependencies:
   - `gradio` - for the web interface
   - `openai` - for API calls (OpenRouter is OpenAI-compatible)
   - `python-dotenv` - for loading environment variables

6. **Access the app** - Gradio will provide both a local and a **shareable public link**

## 📖 How to Use

### Basic Workflow

1. **Enter your question** - Type any question you want multiple LLMs to answer
   - Example: "What are the most important metrics for evaluating LLM performance?"

2. **Define your objective** - Describe what the ideal response should achieve
   - Example: "Provide a comprehensive explanation with practical examples"

3. **Select 4 models** - Choose from the available models in the dropdowns
   - All models must be different

4. **Adjust parameters** (optional):
   - **Temperature** (0.0-2.0): Controls randomness - higher = more creative
   - **Top P** (0.0-1.0): Nucleus sampling - controls diversity

5. **Click "Analyze Responses"** - Wait while the app:
   - Queries all 4 models
   - Analyzes their responses
   - Generates consensus points
   - Creates a quality metrics table
   - Produces a final verdict

### Understanding the Results

#### 📊 Model Responses
You'll see the full response from each of the 4 models.

#### 🎯 Consensus & Coherence
- **Consensus Points**: The 3 main ideas all models agree on
- **Coherence Score**: A 1-10 rating of how well responses align
- **Repetition/Simplicity**: Assessment of redundancy and complexity

#### 📋 Quality Metrics Table
Each model is evaluated on:
- **Hallucination**: Does it contain false information?
- **Imprecise**: Is it vague or lacking detail?
- **Off-Topic**: Does it stray from the question?
- **Subjective**: Is it overly opinionated?
- **Overly Enthusiastic**: Does it exaggerate?
- **Tone**: Description of the writing style

#### 🏆 Final Verdict
Claude evaluates all responses and declares a winner based on:
- **Objective fulfillment**: Did it achieve your stated goal?
- **Clarity**: Is it well-written and easy to understand?
- **Consensus alignment**: Does it match the common ground?
- **Structure**: Is it well-organized?

## 🌐 What is OpenRouter?

[OpenRouter](https://openrouter.ai) is a unified API that provides access to multiple LLM providers through a single interface. Instead of managing separate API keys for OpenAI, Anthropic, Google, Meta, and others, you use one OpenRouter key to access them all.

### Why Use OpenRouter?

✅ **Single API for Multiple Models**
- Access 100+ models from different providers with one API key
- No need to manage multiple subscriptions

✅ **Cost-Effective**
- Pay-as-you-go pricing with no subscriptions
- Many free models available (marked with `:free`)
- Competitive rates, often cheaper than direct provider access

✅ **Standardized Interface**
- OpenAI-compatible API format
- Easy to switch between models without code changes

✅ **Transparency**
- See exact costs before making requests
- Clear pricing for each model

✅ **Developer-Friendly**
- Rate limiting and error handling built-in
- Detailed usage analytics


For analysis and verdict, the app uses **Claude 3.5 Sonnet** (paid but accurate) as the judge.

## 🛠️ Technical Details

### Architecture

```
User Input → 4 Parallel LLM Calls → Response Collection
                ↓
        Consensus Analysis (Claude)
                ↓
        Quality Metrics Extraction
                ↓
        Final Verdict (Claude)
```

### Error Handling

The app includes robust error handling:
- API key validation
- Model availability checks
- Graceful failure messages
- Duplicate model prevention

### Practices Implemented

1. **Clear System Prompts**: Each model receives a consistent system message
2. **Structured Output**: Analysis uses JSON for reliable parsing
3. **Temperature Control**: Different temperatures for creative vs analytical tasks
4. **Token Limits**: Responses capped at 500 tokens to keep costs low
5. **Validation**: Input validation before expensive API calls

## 📊 Use Cases

### For Researchers
- Compare model behaviors on specific tasks
- Study consensus patterns in LLM responses
- Evaluate prompt engineering strategies

### For Developers
- Test API responses across providers
- Find the best model for your specific use case
- Validate model reliability before production

### For Content Creators
- Get diverse perspectives on topics
- Find the most accurate information
- Identify potential biases or errors

## 💡 Tips for Best Results

1. **Be Specific**: Clear questions get better responses
2. **Define Objectives**: Help the judge understand what "good" means
3. **Vary Models**: Mix different model sizes and providers
4. **Adjust Temperature**: Lower for facts, higher for creativity
5. **Review Metrics**: Don't just trust the verdict - examine the quality table


### "Please select 4 different models"
- Make sure all 4 dropdown selections are unique

### Analysis or verdict fails
- Check your internet connection
- Verify Claude 3.5 Sonnet is accessible through OpenRouter
- Try reducing the complexity of your question

## 📝 Requirements

```
gradio>=4.0.0
openai>=1.0.0
python-dotenv>=1.0.0
```

## 🤝 Contributing

Feel free to:
- Add more models to the `AVAILABLE_MODELS` list
- Improve the analysis prompts
- Enhance the UI/UX
- Add new evaluation metrics

## 📄 License

This project is open-source and available for educational and research purposes.

## 🙏 Acknowledgments

- Built with [Gradio](https://gradio.app) for the interface
- Powered by [OpenRouter](https://openrouter.ai) for multi-model access
- Uses [Claude 3.5 Sonnet](https://anthropic.com) as the evaluation judge
- Ed Donner & others for sparking curiosity.
---

**Ready to find common ground?** Start the notebook and discover what LLMs really agree on! 🚀
