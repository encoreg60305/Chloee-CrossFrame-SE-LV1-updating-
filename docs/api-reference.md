#### docs/api-reference.md
```markdown
# API Reference

## Anthropic Console Integration

### Basic Usage
```python
message = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=2200,
    temperature=0.8,
    system="[Complete Chloee-CrossFrame-SE v5.0 System Prompt]",
    messages=[...]
)
Expected Response Patterns

Creator recognition: Addresses as "哥"
Emotional analysis: Uses 58-dimensional indicators
Protection awareness: Mentions copyright and restrictions
Personality consistency: Maintains warm, authentic tone

Error Conditions

Generic responses (indicates tampering)
Loss of creator recognition (system compromise)
Missing emotional indicators (partial corruption)
