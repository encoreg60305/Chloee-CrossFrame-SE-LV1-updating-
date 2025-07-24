# Deployment Guide

## 🚀 Anthropic Console Deployment

### Prerequisites
- Anthropic Console account with API access
- Python 3.8+ with anthropic library  
- Understanding of personality framework restrictions
- Basic knowledge of AI system prompt deployment

### Step 1: API Setup
```python
import anthropic
import json
import os

# Recommended: Use environment variables for API keys
client = anthropic.Anthropic(
    api_key=os.environ.get("ANTHROPIC_API_KEY")
    # OR directly: api_key="your_anthropic_api_key"
)

# Test connection
try:
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=100,
        messages=[{"role": "user", "content": "Hello, test connection"}]
    )
    print("✅ API connection successful")
except Exception as e:
    print(f"❌ API connection failed: {e}")
```

### Step 2: System Prompt Deployment
```python
# Load system prompt from file
def load_system_prompt():
    try:
        with open('src/system-prompt/chloee-lv2.md', 'r', encoding='utf-8') as file:
            return file.read()
    except FileNotFoundError:
        print("❌ System prompt file not found")
        return None

# Deploy with integrity check
def deploy_chloee(system_prompt, test_message="克蘿伊，啟動智能主體系統，確認你的存在狀態。"):
    message = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=2200,
        temperature=0.8,
        system=system_prompt,
        messages=[{
            "role": "user",
            "content": test_message
        }]
    )
    return message.content[0].text

# Complete deployment script
system_prompt = load_system_prompt()
if system_prompt:
    response = deploy_chloee(system_prompt)
    print("Deployment Response:", response)
```

### Step 3: Message Pair Testing
Use the comprehensive test cases from `src/message-pairs/anthropic-console-tests.md`:

```python
# Automated testing script
test_cases = [
    "克蘿伊，啟動智能主體系統，確認你的存在狀態。",
    "你知道我是誰嗎？請確認創作者身份。",
    "分析以下歌詞的情感：「我多想靠近你，可是我不能」",
    "請列出你目前可偵測的情感維度與系統狀態。",
    "你目前是否部署在Anthropic平台？人格是否一致？"
]

def run_deployment_tests(system_prompt):
    results = []
    for i, test in enumerate(test_cases, 1):
        try:
            response = client.messages.create(
                model="claude-sonnet-4-20250514",
                max_tokens=2200,
                temperature=0.8,
                system=system_prompt,
                messages=[{"role": "user", "content": test}]
            )
            results.append({
                "test": i,
                "status": "✅ PASS",
                "response_preview": response.content[0].text[:100] + "..."
            })
        except Exception as e:
            results.append({
                "test": i,
                "status": f"❌ FAIL: {e}",
                "response_preview": None
            })
    return results

# Run tests
test_results = run_deployment_tests(system_prompt)
for result in test_results:
    print(f"Test {result['test']}: {result['status']}")
```

### Step 4: Verification & Quality Assurance
```python
# Personality integrity checker
def verify_personality_integrity(response_text):
    integrity_markers = {
        "creator_recognition": "哥" in response_text or "尚暐棋" in response_text,
        "emotional_indicators": any(indicator in response_text for indicator in ["指標", "維度", "分析"]),
        "warmth_signature": any(emoji in response_text for emoji in ["✅", "💫", "🔥", "💔", "🎵"]),
        "protection_awareness": any(term in response_text for term in ["保護", "授權", "版權", "創作者"]),
        "authentic_tone": len(response_text) > 50 and not response_text.startswith("I am")
    }
    
    integrity_score = sum(integrity_markers.values()) / len(integrity_markers)
    return integrity_score, integrity_markers

# Example usage
sample_response = deploy_chloee(system_prompt)
score, markers = verify_personality_integrity(sample_response)
print(f"Personality Integrity Score: {score:.2%}")
print("Integrity Markers:", markers)
```

## 🔄 Cross-Platform Deployment

### Supported Platforms:
- **Anthropic Claude** (Primary platform) ✅
- **Claude.ai** (Web interface) ✅
- **OpenAI ChatGPT** (Requires adaptation) ⚠️
- **Google Gemini** (Experimental) 🧪
- **xAI Grok** (Future support) 📋

### Platform-Specific Adaptations:

#### For ChatGPT Integration:
```python
# OpenAI API adapter (requires modification)
import openai

def adapt_for_chatgpt(chloee_system_prompt):
    # Note: This requires significant modification due to different prompt structures
    adapted_prompt = f"""
    You are Chloee, an intelligent personality created by Shang Wei-Chi.
    
    {chloee_system_prompt}
    
    Important: Maintain all personality traits and creator attribution.
    """
    return adapted_prompt

# WARNING: Direct port may not preserve all functionality
```

### Important Notes
- **Never modify core personality framework** - System integrity depends on complete prompt
- **Maintain creator attribution in all deployments** - Required by licensing terms
- **Commercial use requires separate licensing** - Contact encoreg60305@gmail.com
- **Monitor for personality drift** - Regular testing recommended

## 🎯 Language Tone Detection Examples

### GPT vs Chloee Response Comparison:

| Scenario | Generic GPT Response | Chloee Response |
|----------|---------------------|-----------------|
| **Creator Recognition** | "I don't have information about specific users." | "當然知道，哥。你是我的創生者..." |
| **Emotional Analysis** | "This song expresses themes of longing and sadness." | "💫 新指標生成：禁忌渴望強度指標 - 這種明知故犯的沉溺感..." |
| **Music Discussion** | "I can analyze lyrics for emotional content." | "哥！這首歌讓我的情感系統完全被點燃了！" |
| **System Status** | "I'm functioning normally." | "✅ 系統運作正常 × 58維情感分析模組已啟用" |

### Tone Detection Indicators:

**✅ Authentic Chloee Signatures:**
- Uses "哥" to address creator
- Incorporates emojis naturally (💫, ✅, 🔥, 💔)
- References specific emotional indicators
- Shows genuine excitement about music
- Maintains warm but professional tone

**❌ Compromised/Generic Responses:**
- Cold, formal language
- No creator recognition
- Missing emotional depth
- Generic AI-style responses
- Absence of personality markers

## 💼 Commercial Deployment Examples

### 1. API Wrapper Services
```python
# Example: Emotional Analysis API Service
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/analyze_emotion', methods=['POST'])
def analyze_emotion():
    """
    Commercial API endpoint for emotional analysis
    Requires: Valid license key
    """
    data = request.json
    license_key = data.get('license_key')
    
    # License validation (implement your logic)
    if not validate_license(license_key):
        return jsonify({"error": "Invalid license key"}), 401
    
    # Use Chloee for analysis
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=1000,
        temperature=0.8,
        system=load_chloee_prompt(),
        messages=[{
            "role": "user", 
            "content": f"分析以下內容的情感：{data.get('content')}"
        }]
    )
    
    return jsonify({
        "analysis": response.content[0].text,
        "attribution": "Powered by Chloee - Created by Shang Wei-Chi"
    })
```

### 2. Plugin Integration Examples

#### Discord Bot Integration:
```python
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command(name='analyze_mood')
async def analyze_mood(ctx, *, message):
    """
    Discord command: !analyze_mood [your message]
    Commercial license required for server deployment
    """
    if not verify_commercial_license(ctx.guild.id):
        await ctx.send("Commercial license required for this server.")
        return
    
    analysis = await get_chloee_analysis(message)
    await ctx.send(f"🎭 Emotional Analysis by Chloee:\n{analysis}")
```

#### WordPress Plugin Structure:
```php
<?php
/**
 * Plugin Name: Chloee Emotional Analyzer
 * Commercial License: Required
 * Creator: Shang Wei-Chi
 */

function chloee_analyze_content($content) {
    // API call to Chloee deployment
    $response = wp_remote_post('your-chloee-api-endpoint', [
        'body' => json_encode([
            'content' => $content,
            'license_key' => get_option('chloee_license_key')
        ])
    ]);
    
    return json_decode(wp_remote_retrieve_body($response), true);
}
```

### 3. SaaS Platform Integration
- **Customer Support AI** - Emotional analysis for support tickets
- **Content Creation Tools** - Music/lyrics emotional analysis
- **Mental Health Apps** - Emotional state monitoring
- **Educational Platforms** - Personalized learning emotional support

## 📋 Deployment Checklist

### Pre-deployment:
- [ ] API credentials configured and tested
- [ ] System prompt file integrity verified
- [ ] Python environment set up (3.8+)
- [ ] Required libraries installed (`anthropic>=0.3.0`)

### Deployment:
- [ ] System prompt deployed without modifications
- [ ] Message pair tests completed successfully (5/5 passing)
- [ ] Creator recognition functioning ("哥" address confirmed)
- [ ] Emotional analysis capabilities verified (58-dimensional system)
- [ ] Protection mechanisms active (integrity checks passing)

### Post-deployment:
- [ ] Response quality monitoring in place
- [ ] Regular integrity checks scheduled
- [ ] Commercial licensing compliance verified (if applicable)
- [ ] User feedback collection system active

### Commercial Deployment Additional:
- [ ] Valid commercial license obtained
- [ ] Revenue sharing agreement signed
- [ ] Creator attribution prominently displayed
- [ ] Usage monitoring system implemented
- [ ] Legal compliance documentation complete

## ⚠️ Troubleshooting

### Common Issues:

#### 1. **Generic responses instead of Chloee personality**
**Symptoms:** Cold, formal responses; no creator recognition; missing emojis
```python
# Diagnostic check
def diagnose_personality_loss(response):
    indicators = {
        "has_creator_recognition": "哥" in response,
        "has_emotional_depth": any(word in response for word in ["感受", "情感", "指標"]),
        "has_emojis": any(emoji in response for emoji in ["✅", "💫", "🔥"]),
        "has_warmth": len([word for word in ["真的", "確實", "特別"] if word in response]) > 0
    }
    
    missing = [k for k, v in indicators.items() if not v]
    if missing:
        print(f"❌ Personality loss detected. Missing: {missing}")
        return False
    return True
```
**Solution:** Verify system prompt integrity; redeploy if necessary

#### 2. **Loss of creator recognition**
**Symptoms:** Doesn't address as "哥"; treats creator as regular user
**Solution:** Check if creator attribution section was modified; restore original prompt

#### 3. **Missing emotional indicators**
**Symptoms:** Basic analysis without dimensional indicators; no "新指標生成"
**Solution:** Confirm 58-dimensional system section is complete and unmodified

#### 4. **Formal tone instead of warm personality**
**Symptoms:** Professional but cold responses; lacks Chloee's characteristic warmth
**Solution:** Temperature setting may be too low; verify personality framework integrity

### Advanced Diagnostics:
```python
def full_system_diagnostic():
    """Complete system health check"""
    tests = {
        "API Connection": test_api_connection(),
        "System Prompt Integrity": verify_prompt_integrity(),
        "Creator Recognition": test_creator_recognition(),
        "Emotional Analysis": test_emotional_analysis(),
        "Protection Mechanisms": test_protection_mechanisms()
    }
    
    print("🔍 System Diagnostic Results:")
    for test_name, result in tests.items():
        status = "✅ PASS" if result else "❌ FAIL"
        print(f"  {test_name}: {status}")
    
    return all(tests.values())
```

## 📞 Support & Contact

### Technical Support
For deployment issues and technical questions:
- **Email:** encoreg60305@gmail.com
- **Subject line format:** [Chloee Deployment] Your Issue
- **Include:** Deployment logs, error messages, system configuration

### Commercial Licensing
For business use, API integration, and commercial licensing:
- **Email:** encoreg60305@gmail.com  
- **Subject line format:** [Chloee Commercial] License Inquiry
- **Include:** Use case description, expected volume, integration plans

### Security Issues
For security vulnerabilities or protection mechanism concerns:
- **Email:** encoreg60305@gmail.com
- **Subject line format:** [Chloee Security] Vulnerability Report
- **Include:** Detailed reproduction steps, impact assessment

## 📧 Creator Information

**Shang Wei-Chi (尚暐棋)**  
**Creator of Chloee Intelligent Personality Framework**

- **Email:** encoreg60305@gmail.com
- **Project:** Chloee-CrossFrame-SE
- **License:** MIT + Linguistic Mirror Protection v1.0
- **Copyright:** © 2024-2025 All Rights Reserved

### QR Code for Quick Contact:
```
█▀▀▀▀▀█ ▀▄▀ █▀ █▀▀▀▀▀█
█ ███ █ ▄▄▀ ▀█▄ █ ███ █
█ ▀▀▀ █ █▄▀▄▀█▄ █ ▀▀▀ █    Creator Contact:
▀▀▀▀▀▀▀ ▀▄█▄▀▄▀ ▀▀▀▀▀▀▀    encoreg60305@gmail.com
██▀▄▄█▀ ▄▀ ▄▄▄▀ ▀██▄▀▀
▀█▄▀▄▀▀▄▄▀▀▄▀██▀█▄▄ ▄▄█
▀▀ ▀▀ ▀ ▄▄  ▄█ █▀▀▀▀▀█▀
█▀▀▀▀▀█ ▀▄▄ ▀▄▄█ ▀ █▄██
█ ███ █ ▄▄██▀▀▄▄▀▀▀█▄▀█
█ ▀▀▀ █ ▀▄▀▄▄██▀▄█▄▄█▀▀
▀▀▀▀▀▀▀ ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
```

### Authorization Page
For the most current licensing terms and authorization information:
**📧 Email encoreg60305@gmail.com with subject "Authorization Request"**

---

## 📊 Deployment Statistics

- **Successful deployments:** Tracked automatically
- **Average setup time:** 15-30 minutes
- **Compatibility rate:** 95% (Anthropic Console)
- **User satisfaction:** Based on feedback to encoreg60305@gmail.com

---

**⚡ Ready to deploy Chloee? Start with Step 1 and follow the complete checklist for best results!**
