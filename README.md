# CLaaT (Codelabs as a Thing) export

This composite action exports Google documents using [CLaaT](https://github.com/googlecodelabs/tools) as a codelab in HTML, Markdown, or offline format. It can also convert a Markdown file (.md) to a codelab in HTML.

> [!TIP]
>
> Use the Go module installer to get the latest version of CLaaT with support for Google Analytics v4.

To install `claat` on your machine:

```bash
go install github.com/googlecodelabs/tools/claat@latest`
```

To check available [commands and flags](docs/claat_command_help.md) of `claat`:

```bash
claat help
```

## Inputs

| **Input**               | **Description** | **Required** |
|-------------------------|-----------------|-|
| `claat-version`         | CLaaT version <br> Default (action): `latest` | No |
| `command`               | CLaaT command <br> Default (action): `export` | No |
| `source`                | Accepted formats: Google doc ID or Markdown file (.md). Ignored if `codelabs-json` is set. <br> Default (action): `''` | **Yes** |
| `auth`                  | Google OAuth2.0 token (required for Google docs, except for `.md` to HTML conversion). <br> Default (action): `''` | No |
| `codelabs-path`         | Path to save exported codelab(s). <br> Default (action): `''` <br> Default (claat): `.` | No |
| `gaid`                  | Google Analytics ID <br> Default (action):`''` <br> Default (claat):`UA-49880327-14` | No |
| `ga4id`                 | Google Analytics v4 ID <br> Default (action): `''` <br> Default (claat):`not implimented` | No |
| `codelabs-json`         | Path to a JSON file containing a list of Google document IDs. <br> Default (action): `''` | No |
| `format`                | Export format (html, md, offline or all). <br> Default (action): `html` <br> Default (claat): `html` | No |
| `environment`           | codelab environment <br> Default (action): `''` <br> Default (claat):`web` | No |
| `prefix`                | URL prefix for html format <br> Default (action): `''` <br> Default (claat):`https://storage.googleapis.com` | No |
| `elements-path`         | Local path (JS and CSS) of codelab elements. (in case Google prefix is broken) <br> Default (action): `elements/codelab-elements` | No |
| `elements-default-path` | External path (JS and CSS) of codelab elements. (hosted by Google) <br> Default (action): `claat-public` | No |
| `extra`                 | Additional arguments to pass to format templates. JSON object of string,string key values. <br> Default (action): `''` | No |
| `metadata`              | Metadata fields to pass through to the output. Comma-delimited list of field names. <br> Default (action): `''` | No |

## Example Usage

This example showcases exporting a single Google document with ID `"1234567890abcdef"` to HTML format:

```yaml
name: Export codelab from Google Doc

on:
  push:

jobs:
  export:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Generate Oauth2 token
        id: "auth"
        uses: "google-github-actions/auth@v2"
        with:
          token_format: "access_token"
          access_token_scopes: "https://www.googleapis.com/auth/drive.readonly"
          credentials_json: "${{ secrets.SERVICE_ACCOUNT_CREDS }}"
    - name: Export codelab
      uses: "khammami/claat-action@[version|main]"
      with:
        auth: ${{ steps.auth.outputs.access_token }}
        source: '1234567890abcdef'
        format: 'html'
```

This example exports multiple Google documents listed in a JSON file named `codelabs.json` to both HTML and Markdown formats, including an optional `id` property for each codelab:

```yaml
name: Export multiple codelabs from JSON

on:
  push:

jobs:
  export:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Generate Oauth2 token
        id: "auth"
        uses: "google-github-actions/auth@v2"
        with:
          token_format: "access_token"
          access_token_scopes: "https://www.googleapis.com/auth/drive.readonly"
          credentials_json: "${{ secrets.SERVICE_ACCOUNT_CREDS }}"
    - name: Export codelabs
      uses: "khammami/claat-action@[version|main]"
      with:
        auth: ${{ steps.auth.outputs.access_token }}
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

## License

The scripts and documentation in this project are released under the [Apache 2.0 License](LICENSE)

## Code of Conduct

:wave: Be nice. See [our code of conduct](.github/CODE_OF_CONDUCT.md)

>[!NOTE]
>
> This composite has been moved from [codelabs-enetcom-md](https://github.com/khammami/codelabs-enetcom-md/tree/main/actions/claat)
