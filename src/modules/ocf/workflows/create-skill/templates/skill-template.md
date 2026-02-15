---
name: {{skill_name}}
description: "{{skill_description}}"
metadata:
  {
    "openclaw":
      {
        "emoji": "{{emoji}}",
        {{#if requires}}
        "requires": {{requires_block}},
        {{/if}}
        {{#if install}}
        "install": {{install_block}},
        {{/if}}
      },
  }
---

# {{skill_title}}

{{skill_body}}
