This utility generates an html file from a MD file for an open-tezos task.

# Install

```
npm i -g @completium/open-tezos-md-task-util@latest
```

# Run

The package installs the binary `mdtask2html`:

```
$ mdtask2html test.md > index.html
```

# Features

## Task metadata

It supports frontMatter style PEM task medata. For example:

```
---
id : example
authors : [john.doe@mycompany.com]
---

# MD content here

```

PEM task metadata are defaulted to:
```json
{
  "license" : "MIT",
  "language" : "en",
  "version": "0.1",
  "baseUrl" : "",
  "supportedLanguages": ["michelson", "ligo", "mligo", "religo", "jsligo", "smartpy", "archetype"],
  "hasUserTests": "false",
  "testMode": "false",
  "limits" : {
    "*": {"time": "60000", "memory": "60000"}
  },
  "common" : "../../_common"
}
```

## Language specific elements

The main feature is to dedicate an task element to a specific language, that is an element that is displayed only for the selected language : paragraph, inlined text, link, code block.

The following language tags are supported: `michelson`,`'ligo`, `mligo`, `religo`, `jsligo`, `smartpy` and `archetype`.

### Paragraph

The following md code:

```md
<archetype>

Some content specific to Archetype

</archetype>
```

is compiled to:

```html
<div select-lang="archetype" data-lang="archetype">
  <p>
    Some content specific to Archetype
  </p>
</div>
```

### Inlined text

The following md code:

```md
This is [inlined content specific to archetype](archetype).
```

is compiled to:

```html
<p>
This is
<span select-lang="archetype" data-lang="archetype">
  inlined content specific to archetype
</span>
</p>
```

### Code block

Language is specified with standard triple back quote followed by language id; for example:

    ```archetype
    archetype test

    variable counter : nat = 0
    ```

This is compiled to

```html
<div select-lang="archetype" data-lang="archetype" data-show-source="true" data-code="archetype test

variable counter : nat = 0">
</div>
```

### Link

It is possible to specify the language associated to a link by adding the language identifier after the url. For example, to display the link for archetype language:

    [doc](https://archetype-lang.org/ "archetype")

This is compiled to:

```html
<a href="https://archetype-lang.org/" target="_blank" rel="noopener noreferrer" select-lang="archetype" data-lang="archetype">doc</a>
```

## Admonitions

5 types of admonitions are supported: `info`, `note`, `tip`, `caution`, `danger`

For example:

```md
:::info
This is some information
:::
```

This is compiled to:
```html
<div admonition admonition-type="info"><p>This is some info</p></div>
```

## Katex equations

Katex equation is available; for example:

```md
$$ (a+b)^2 = a^2 + 2*a*b + b^2 $$
```

This is compiled to:
```html
<span class="math math-inline">(a+b)^2 = a^2 + 2*a*b + b^2</span>
```

## HTML tags

It supports basic html tags (`div`, `pre`, `code`, ...). For example to add the language selector:

```md
Choose your language : <div select-lang-selector="true" />
```


