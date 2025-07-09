# GPT-based SCALE Framework: Home Energy Conversation Analysis

## Overview

The GPT-based SCALE (Structured Context-Aware Language Evaluation) Framework is an advanced LLM-based system designed to analyze conversations between users and AI assistants about home energy analysis. This framework uses experimental context-aware analysis to distinguish between authentic user engagement and data-enhanced assistant responses.

## Key Features

### 🧠 **Experimental Context-Aware Analysis**
- Distinguishes between authentic user engagement and data-enhanced assistant analysis
- Applies different evaluation criteria for users vs. AI assistants
- Accounts for experimental settings where users are provided energy data by researchers

### 📊 **Multi-Factor Confidence Scoring**
- **Explicitness (30%)**: How directly concepts are mentioned using appropriate terminology
- **Depth (25%)**: Quality and authenticity of engagement with concepts
- **Consideration (25%)**: Whether concepts meaningfully influenced thinking
- **Evidence (20%)**: Quality of supporting evidence provided

### 🗣️ **User Engagement Contextual Metrics**
Detects 4 engagement patterns based on speech act theory:
- **Information Seeking**: Directive acts aimed at obtaining information
- **Constraint Articulation**: Stating personal limitations or boundaries
- **Solution Evaluation**: Expressing judgments about proposed solutions
- **Commitment Expression**: Willingness to try solutions or make changes

### 🔍 **Home Energy Use Analysis Evaluation**
Analyzes 7 energy-related concepts:
- **Energy Consumption**: Discussion of appliance/circuit energy usage data
- **Cost Awareness**: Electricity bills, utility rates, time-of-use pricing
- **Behavioral Change**: Adjusting usage patterns and energy-saving behaviors
- **Use Flexibility**: How regularly/irregularly appliances are used
- **Use Frequency**: How often appliances are operated
- **Comfort Association**: Comfort/convenience considerations for energy decisions
- **Technical Knowledge**: Understanding of how appliances and systems work

## Installation

### Prerequisites
- Python 3.8+
- OpenAI API key
- Required packages (install via pip):

```bash
pip install pandas numpy scikit-learn textstat matplotlib seaborn openai python-dotenv
```

### Setup
1. Clone or download the `SCALE_framework.ipynb` file
2. Create a `.env` file in the same directory with your OpenAI API key:
```
OPENAI_API_KEY=your-openai-api-key-here
```

## Usage

### Quick Start - Single Conversation Analysis

```python
# Analyze a single conversation file
results = analyze_single_conversation_llm(
    file_path="./Data/020/EntireConversation_extracted.json",
    detection_threshold=0.4,  # Confidence threshold for concept detection
    analysis_model="gpt-4o-mini"  # OpenAI model to use
)
```

### Batch Processing

```python
# Process all conversations in a data folder
results = run_batch_analysis(
    data_folder="./Data",
    detection_threshold=0.4,
    analysis_model="gpt-4o-mini"
)

# Process a specific range of subjects (e.g., subjects 20-85)
results = process_subject_range(
    start_subject=20,
    end_subject=85,
    data_folder="./Data"
)
```

### Advanced Usage

```python
# Initialize analyzer with custom settings
analyzer = LLMChatAnalyzer(
    api_key="your-api-key",  # Optional if using .env file
    analysis_model="gpt-4o-mini"  # or "gpt-4o", "gpt-4", "gpt-3.5-turbo"
)

# Perform comprehensive analysis
results = analyzer.comprehensive_analysis(
    file_path="conversation.json",
    detection_threshold=0.4
)

# Generate detailed report
report = analyzer.create_detailed_report(results)
print(report)
```

## Data Format

### Input File Structure
Conversations should be in JSON format with the following structure:
```json
[
  {
    "You said": "User message content...",
    "ChatGPT said": "Assistant response content..."
  },
  {
    "You said": "Next user message...",
    "ChatGPT said": "Next assistant response..."
  }
]
```

### Expected Directory Structure
```
Data/
├── 001/
│   └── EntireConversation_extracted.json
├── 002/
│   └── EntireConversation_extracted.json
└── ...
```

## Output

### Individual Analysis Results
Each conversation generates:
- **JSON file**: Complete analysis with confidence scores and evidence
- **Detailed report**: Human-readable summary with factor breakdowns
- **Concept attribution**: Which participant introduced each concept

### Batch Processing Results
- **batch_analysis_results.json**: Complete aggregated results
- **batch_summary.csv**: Overview statistics per conversation
- **concept_frequencies.csv**: Frequency of concepts across all conversations

### Sample Output Structure
```json
{
  "subject_id": "020",
  "analysis_framework": "experimental_context_aware_multi_factor",
  "user_concepts": {
    "energy_cost_awareness": {
      "detected": true,
      "confidence": 0.660,
      "factor_scores": {
        "explicitness": {"score": 0.80, "justification": "..."},
        "depth": {"score": 0.60, "justification": "..."},
        "consideration": {"score": 0.80, "justification": "..."},
        "evidence": {"score": 0.40, "justification": "..."}
      },
      "evidence_quote": "I want to reduce my energy bills...",
      "overall_reasoning": "User actively engaged in cost discussions...",
      "analysis_type": "authentic_engagement"
    }
  },
  "gpt_concepts": { /* Similar structure for assistant analysis */ },
  "conversation_metadata": { /* Turn counts, word counts, etc. */ },
  "user_engagement": { /* Engagement metrics */ }
}
```

## Configuration Options

### Detection Threshold
- **0.4 (default)**: Balanced detection - moderate confidence required
- **0.3**: More liberal detection - lower confidence threshold
- **0.5**: Conservative detection - higher confidence required

### Analysis Models
- **gpt-4o-mini (recommended)**: Fast, cost-effective, good performance
- **gpt-4o**: Slower, more expensive, best performance
- **gpt-4**: High quality but more expensive
- **gpt-3.5-turbo**: Fastest and cheapest, decent performance

## Key Components

### LLMChatAnalyzer Class
Main analysis engine with methods:
- `analyze_concepts_with_llm()`: Core concept detection using LLM
- `comprehensive_analysis()`: Complete analysis of a conversation
- `create_detailed_report()`: Generate human-readable reports
- `export_results()`: Save results to files

### Scoring Framework
The experimental context-aware scoring considers:
- **User criteria**: Focus on authentic engagement, personal constraints, genuine questions
- **Assistant criteria**: Data analysis quality, domain expertise, practical guidance
- **Weighted combination**: Balanced assessment across multiple factors

## Research Applications

This framework is designed for research into:
- **Human-AI interaction patterns** in domain-specific conversations
- **Authentic user engagement** vs. data-driven AI responses
- **Energy behavior change** through conversational AI
- **Concept introduction and adoption** in educational dialogues

## Performance Notes

- **Processing time**: ~60-300 seconds per conversation (depending on length and model)
- **API costs**: Approximately $0.01-0.05 per conversation with gpt-4o-mini
- **Batch processing**: Supports large-scale analysis with progress tracking
- **Error handling**: Robust retry mechanisms and graceful failure handling

## Limitations

- Requires OpenAI API access and associated costs
- Analysis quality depends on the chosen LLM model
- Designed specifically for energy efficiency conversations
- Experimental framework - results should be validated for your use case

## Citation

If you use this framework in research, please cite appropriately and note that this is an experimental context-aware analysis system designed for distinguishing authentic user engagement from data-enhanced AI responses.

## Support

For issues or questions:
1. Check that your OpenAI API key is correctly configured
2. Ensure input files match the expected JSON format
3. Verify that the data directory structure is correct
4. Review the console output for specific error messages

## License

[Add your license information here]