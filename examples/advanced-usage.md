#### examples/advanced-usage.md
```markdown
# Advanced Usage Examples

## Commercial Licensing Integration
```python
# For authorized commercial users
system_prompt = load_system_prompt_with_license_key(
    license_key="your_commercial_license",
    attribution_mode="prominent_display"
)
Cross-Platform Deployment
python# Adapting for different platforms
def adapt_for_platform(platform_type, base_prompt):
    if platform_type == "claude":
        return add_claude_specific_instructions(base_prompt)
    elif platform_type == "gpt":
        return add_gpt_compatibility_layer(base_prompt)
