# CLaaT (Codelabs as a Thing) export

## Description

This composite action exports Google documents using [CLaaT](https://github.com/googlecodelabs/tools) as a codelab in HTML, Markdown, or offline format. It can also convert a Markdown file (.md) to a codelab in HTML.

> [!NOTE]
>
> To check `claat` CLI ,use the Go module installer to get the latest version of CLaaT with support for Google Analytics v4.

To install `claat` on your machine:

```bash
go install github.com/googlecodelabs/tools/claat@latest`
```

To check available commands and flags of `claat`:

```bash
claat help
```

## Inputs

| **Input** | **Description** | **Default** | **Required** |
|---|---|---|---|
| `claat-version` | CLaaT version | `latest` | No |
| `source` | Accepted formats: Google doc ID or Markdown file (.md). Ignored if `codelabs-json` is set. | | **Yes** |
| `auth` | Google OAuth2.0 token (required for Google docs, except for .md to HTML conversion). | `''` (empty string) | No |
| `codelabs-path` | Path to save exported codelab(s). | `codelabs` | No |
| `gaid` | Google Analytics ID | `UA-3295395-7` | No |
| `ga4id` | Google Analytics v4 ID | `G-E0H6JSF2N3` | No |
| `codelabs-json` | Path to a JSON file containing a list of Google document IDs. | `''` (empty string) | No |
| `format` | Export format (html, md, or all). | `html` | No |

## Example Usage

This example showcases exporting a single Google document with ID `"1234567890abcdef"` to HTML format:

```yaml
name: Export codelab from Google Doc

on:
  push: {}

jobs:
  export:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Export codelab
      uses: "khammami/codelabs-enetcom-md/actions/claat@v0"
      with:
        source: '1234567890abcdef'
        format: 'html'
```

This example exports multiple Google documents listed in a JSON file named `codelabs.json` to both HTML and Markdown formats, including an optional `id` property for each codelab:

```yaml
name: Export multiple codelabs from JSON

on:
  push: {}

jobs:
  export:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Export codelabs
      uses: "khammami/codelabs-enetcom-md/actions/claat@v0"
      with:
        codelabs-json: 'codelabs.json'
        format: 'all'
```

`codelabs.json`:

```json
[
  {
    "id": "codelab-1",
    "source": "Google document ID"
  },
  {
    "id": "codelab-2",
    "source": "path/codelab.md"
  }
]
```

>[!NOTE]
>
> Remember to replace the example Google document ID and JSON file path with your actual values. You can also adjust the `auth`, `codelabs-path`, `gaid`, and `ga4id` inputs as needed
