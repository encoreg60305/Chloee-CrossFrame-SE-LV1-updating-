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
