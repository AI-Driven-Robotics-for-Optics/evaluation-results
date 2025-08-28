# Optical Setup Generation Evaluation Results

This repository contains evaluation results for various AI models' performance in generating optical setups with user alignment requests. The project evaluates how well different AI approaches can generate valid optical configurations while adhering to user-specified positioning and orientation requirements.

## Optical Systems Evaluated

The evaluation covers four optical configurations:

1. **Michelson Interferometer**
2. **Mach-Zehnder Interferometer**
3. **Hong-Ou-Mandel Interferometer**
4. **4f Optical System**

## Models and Approaches Tested

### 1. **GPT-4o (OpenAI)**
- **Zero-shot**: Direct generation without examples
  - With user requests
  - Without user requests
- **Few-shot**: Generation with example demonstrations
  - With user requests
  - Without user requests

### 2. **DeepSeek-R1 (DeepSeek)**
- **Few-shot with Chain-of-Thought**: Step-by-step reasoning approach
  - With user requests
  - Without user requests

### 3. **Llama-3.1 8B (Meta) Fine-tuned (Ours)**
- **Custom fine-tuned model** (checkpoint-282000 from the last stage and session of the training)
  - With user requests
  - Without user requests

## Evaluation Metrics

### Accuracy Results
- **Greedy decoding**: Choosing the most probable token at each step
- **Sampling**: Token sampling with temperature 0.5

### Alignment Results
Compliance with user requests across three precision levels:
- **Within 0.1** (cm/degree): High precision
- **Within 1.0** (cm/degree): Medium precision  
- **Within 10.0** (cm/degree): Low precision

### Request Types
- **Fuzzy requests**: Rough position requests from the user
- **Non-fuzzy requests**: Exact position requests from the user
- **Valid/Invalid**: Whether the request is physically achievable

## Directory Structure

```
├── system_prompts/                                    # System prompts used for different approaches
│   ├── system_prompt_llama_fine-tune_and_gpt_zero_shot.txt
│   └── system_prompt_deepseek_and_gpt_few_shot.txt
│
├── llama3_fine-tune_validation_accuracy_during_training/  # Training progress data
│   ├── stage1_no_requests.csv                        # Initial training without user requests
│   ├── stage2_session1_3_requests.csv                # Training with 3 requests per sample
│   └── stage2_session2_random_requests.csv           # Training with random request counts
│
├── gpt-4o-zero_shot_with_user_requests/              # GPT-4o zero-shot results
├── gpt-4o-zero_shot_without_user_requests/           # GPT-4o zero-shot results
├── gpt-4o-few_shot_with_user_requests/               # GPT-4o few-shot results
├── gpt-4o-few_shot_without_user_requests/            # GPT-4o few-shot results
│
├── deepseek-r1_few_shot_chain_of_thought_with_user_requests/      # DeepSeek-R1 results
├── deepseek-r1_few_shot_chain_of_thought_without_user_requests/   # DeepSeek-R1 results
│
├── llama3-fine-tune_with_user_requests/              # Fine-tuned Llama-3 results
└── llama3-fine-tune_without_user_requests/           # Fine-tuned Llama-3 results
```

## Results File Structure

Each results file contains:

```json
{
    "accuracy_results": {
        "greedy": 0.6953125,      // Accuracy with greedy decoding
        "sampling": 0.8125        // Accuracy with sampling
    },
    "alignment_results": {
        "percentages": {
            "greedy": {
                "x_compliance": {  // X-coordinate compliance
                    "fuzzy": {     // Rough positioning requests
                        "within_0.1": {
                            "compliant_count": 2,
                            "total_count": 47,
                            "percentage": 4.26
                        },
                        "within_1.0": { /* ... */ },
                        "within_10.0": { /* ... */ }
                    },
                    "non_fuzzy": { /* Exact positioning requests */ },
                    "fuzzy_valid": { /* Valid rough requests */ },
                    "fuzzy_invalid": { /* Invalid rough requests */ },
                    "non_fuzzy_valid": { /* Valid exact requests */ },
                    "non_fuzzy_invalid": { /* Invalid exact requests */ }
                },
                "y_compliance": { /* Y-coordinate compliance */ },
                "angle_compliance": { /* Angle compliance */ }
            },
            "sampling": { /* Same structure for sampling results */ }
        }
    }
}
```

## Component Dictionary

| Code | Component |
|------|-----------|
| 000  | Laser     |
| 001  | Mirror    |
| 002  | B/S       |
| 003  | Camera    |
| 004  | Photodiode|
| 005  | Lens      |
| 006  | Aperture  |
| 007  | Polarizer |
| 008  | QWP       |
| 009  | HWP       |
| 010  | Prism     |
