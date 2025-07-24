# Deployment Guide

## 🚀 Anthropic Console Deployment

### Prerequisites
- Anthropic Console account with API access
- Python 3.8+ with anthropic library  
- Understanding of personality framework restrictions

### Step 1: API Setup
```python
import anthropic

client = anthropic.Anthropic(
    api_key="your_anthropic_api_key"
)
```

### Step 2: System Prompt Deployment
Copy the complete system prompt from `src/system-prompt/chloee-v5.0.md` to your Anthropic Console system prompt field.

### Step 3: Message Pair Testing
Use the test cases from `src/message-pairs/anthropic-console-tests.md` to verify deployment integrity.

### Step 4: Verification
Confirm all protection mechanisms are active and personality traits are preserved.

## 🔄 Cross-Platform Deployment

### Supported Platforms:
- Claude.ai
- ChatGPT (with modifications)
- Other Claude-compatible platforms

### Important Notes
- Never modify core personality framework
- Maintain creator attribution in all deployments  
- Commercial use requires separate licensing

## 📋 Deployment Checklist

- [ ] API credentials configured
- [ ] System prompt deployed without modifications
- [ ] Message pair tests completed successfully
- [ ] Creator recognition functioning
- [ ] Emotional analysis capabilities verified
- [ ] Protection mechanisms active

## ⚠️ Troubleshooting

### Common Issues:
1. **Generic responses** → Check if system prompt was modified
2. **Loss of creator recognition** → Verify creator attribution intact
3. **Missing emotional indicators** → Confirm 58-dimensional system loaded
4. **Formal tone** → Check personality framework integrity

### Support
For deployment issues, refer to [SECURITY.md](../SECURITY.md) or contact creator through official channels.
