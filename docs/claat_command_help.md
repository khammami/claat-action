# Output of "claat help"

```console
claat help
Usage: claat <cmd> [options] src [src ...]

Available commands are: export, serve, update, version.

## Export command

Export takes one or more 'src' documents and converts them
to the format specified with -f option.

The following formats are built-in:

- html (Polymer-based app)
- md (Markdown)
- offline (plain HTML markup for offline consumption)

Note that the built-in templates of the formats are not guaranteed to be stable.
They can be found in https://github.com/googlecodelabs/tools/tree/master/claat/render.
Please avoid using default templates in production. Use your own copies.

To use a custom format, specify a local file path to a Go template file.
More info on Go templates: https://golang.org/pkg/text/template/.

Each 'src' can be either a remote HTTP resource or a local file.
Source formats currently supported are:

- Google Doc (Codelab Format, go/codelab-guide)
- Markdown

When 'src' is a Google Doc, it must be specified as a doc ID,
omitting https://docs.google.com/... part.

Instead of writing to an output directory, use "-o -" to specify
stdout. In this case images and metadata are not exported.
When writing to a directory, existing files will be overwritten.

The program exits with non-zero code if at least one src could not be exported.

## Serve command

Serve provides a simple web server for viewing exported codelabs.
It takes no arguments and presents the current directory contents.
Clicking on a directory representing an exported codelab will load
all the required dependencies and render the generated codelab as
it would appear in production.

The serve command takes a -addr host:port option, to specify the
desired hostname or IP address and port number to bind to.

## Update command

Update scans one or more 'src' local directories for codelab.json metadata
files, recursively. A directory containing the metadata file is expected
to be a codelab previously created with the export command.

Current directory is assumed if no 'src' argument is given.

Each found codelab is then re-exported using parameters from the metadata file.
Unused codelab assets will be deleted, as well as the entire codelab directory,
if codelab ID has changed since last update or export.

In the latter case, where codelab ID has changed, the new directory
will be placed alongside the old one. In other words, it will have the same ancestor
as the old one.

While -prefix and -ga can override existing codelab metadata, the other
arguments have no effect during update.

The program does not follow symbolic links and exits with non-zero code
if no metadata found or at least one src could not be updated.

## Flags

  -addr string
    	hostname and port to bind web server to (default "localhost:9090")
  -auth string
    	OAuth2 Bearer token; alternative credentials override.
  -e string
    	codelab environment (default "web")
  -extra string
    	Additional arguments to pass to format templates. JSON object of string,string key values.
  -f string
    	output format (default "html")
  -ga string
    	global Google Analytics account (default "UA-49880327-14")
  -o string
    	output directory or '-' for stdout (default ".")
  -pass_metadata string
    	Metadata fields to pass through to the output. Comma-delimited list of field names.
  -prefix string
    	URL prefix for html format (default "https://storage.googleapis.com")
```
