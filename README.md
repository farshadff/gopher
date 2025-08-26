# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:
# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:

gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true)
fmt.Println("public URL:", u.String())
🟩 pkg/mapext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/mapext"
Functions
Keys[K comparable, V any](m map[K]V) []K

Values[K comparable, V any](m map[K]V) []V

Merge[K comparable, V any](src, ext map[K]V) map[K]V

Example
go
Copy
Edit
out := mapext.Merge(map[string]int{"a":1}, map[string]int{"b":2})
ks  := mapext.Keys(out)   // ["a","b"]
vs  := mapext.Values(out) // [1,2]
🟨 pkg/templateext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/templateext"
Function
Format(tmpl string, model any) (string, error)

Example
go
Copy
Edit
msg, _ := templateext.Format("Hello {{.Name}}!", struct{ Name string }{"World"})
// -> "Hello World!"
🟪 pkg/shell
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/shell"
What it does
Provides helpers for:

Running shell commands

Capturing output and exit codes

Use when you need quick command execution from Go (CI utilities, scaffolding, ops tooling).

🚀 Installation
sh
Copy
Edit
go get github.com/pinosell/gopher@v1.3.16
Import the packages you need:

go
Copy
Edit
import (
  "github.com/pinosell/gopher/pkg/errors"
  "github.com/pinosell/gopher/pkg/s3ext"
  "github.com/pinosell/gopher/pkg/mapext"
  "github.com/pinosell/gopher/pkg/templateext"
  "github.com/pinosell/gopher/pkg/shell"
)
🔗 References
GitHub Repo

pkg.go.dev Documentation

yaml
Copy
Edit

---

Do you want me to also make a **short “Getting Started” example app** (e.g. one `main.go` showing errors + s3 + mapext in action) so you can drop it into the repo as an example?






You said:
please put all in markdown format not outside of markdown


ChatGPT said:
Got it 👍 — here’s the whole thing fully inside Markdown so you can copy-paste straight into an .md file without any extra text:

markdown
Copy
Edit
# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:

gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true






You said:
why you are still putting that outside of the md format . please focus i need all your answer in markdown format 


ChatGPT said:
Understood ✅ — from now on, I’ll put everything strictly inside a Markdown block.
Here’s the full repo documentation, 100% Markdown:

markdown
Copy
Edit
# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:

gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true)
fmt.Println("public URL:", u.String())
🟩 pkg/mapext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/mapext"
Functions
Keys[K comparable, V any](m map[K]V) []K

Values[K comparable, V any](m map[K]V) []V

Merge[K comparable, V any](src, ext map[K]V) map[K]V

Example
go
Copy
Edit
out := mapext.Merge(map[string]int{"a":1}, map[string]int{"b":2})
ks  := mapext.Keys(out)   // ["a","b"]
vs  := mapext.Values(out) // [1,2]
🟨 pkg/templateext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/templateext"
Function
Format(tmpl string, model any) (string, error)

Example
go
Copy
Edit
msg, _ := templateext.Format("Hello {{.Name}}!", struct{ Name string }{"World"})
// -> "Hello World!"
🟪 pkg/shell
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/shell"
What it does
Provides helpers for:

Running shell commands

Capturing output and exit codes

Use when you need quick command execution from Go (CI utilities, scaffolding, ops tooling).

🚀 Installation
sh
Copy
Edit
go get github.com/pinosell/gopher@v1.3.16
Import the packages you need:

go
Copy
Edit
import (
  "github.com/pinosell/gopher/pkg/errors"
  "github.com/pinosell/gopher/pkg/s3ext"
  "github.com/pinosell/gopher/pkg/mapext"
  "github.com/pinosell/gopher/pkg/templateext"
  "github.com/pinosell/gopher/pkg/shell"
)
🔗 References
GitHub Repo

pkg.go.dev Documentation
gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true)
fmt.Println("public URL:", u.String())
🟩 pkg/mapext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/mapext"
Functions
Keys[K comparable, V any](m map[K]V) []K

Values[K comparable, V any](m map[K]V) []V

Merge[K comparable, V any](src, ext map[K]V) map[K]V

Example
go
Copy
Edit
out := mapext.Merge(map[string]int{"a":1}, map[string]int{"b":2})
ks  := mapext.Keys(out)   // ["a","b"]
vs  := mapext.Values(out) // [1,2]
🟨 pkg/templateext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/templateext"
Function
Format(tmpl string, model any) (string, error)

Example
go
Copy
Edit
msg, _ := templateext.Format("Hello {{.Name}}!", struct{ Name string }{"World"})
// -> "Hello World!"
🟪 pkg/shell
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/shell"
What it does
Provides helpers for:

Running shell commands

Capturing output and exit codes

Use when you need quick command execution from Go (CI utilities, scaffolding, ops tooling).

🚀 Installation
sh
Copy
Edit
go get github.com/pinosell/gopher@v1.3.16
Import the packages you need:

go
Copy
Edit
import (
  "github.com/pinosell/gopher/pkg/errors"
  "github.com/pinosell/gopher/pkg/s3ext"
  "github.com/pinosell/gopher/pkg/mapext"
  "github.com/pinosell/gopher/pkg/templateext"
  "github.com/pinosell/gopher/pkg/shell"
)
🔗 References
GitHub Repo

pkg.go.dev Documentation

yaml
Copy
Edit

---

Do you want me to also make a **short “Getting Started” example app** (e.g. one `main.go` showing errors + s3 + mapext in action) so you can drop it into the repo as an example?






You said:
please put all in markdown format not outside of markdown


ChatGPT said:
Got it 👍 — here’s the whole thing fully inside Markdown so you can copy-paste straight into an .md file without any extra text:

markdown
Copy
Edit
# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:

gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true






You said:
why you are still putting that outside of the md format . please focus i need all your answer in markdown format 


ChatGPT said:
Understood ✅ — from now on, I’ll put everything strictly inside a Markdown block.
Here’s the full repo documentation, 100% Markdown:

markdown
Copy
Edit
# Gopher (Go library)

A collection of lightweight Go utility packages: structured errors, S3 helpers, map utilities, templates, and shell command execution.

**Module path:** `github.com/pinosell/gopher`  
**Latest stable release:** v1.3.16 (Aug 30, 2023)  
**License:** MIT  

---

## 📦 Package Overview

pkg/
errors // Rich error type with gRPC + HTTP + i18n hooks
mapext // Helpers for working with Go maps
s3ext // S3 client wrapper (upload/download/delete)
shell // Shell command helpers
templateext // Quick text/template formatter

yaml
Copy
Edit

---

## 🟥 `pkg/errors`

**Import:**  
```go
import gerr "github.com/pinosell/gopher/pkg/errors"
What it does
A structured error type that integrates with:

gRPC codes

HTTP status codes

Localization (i18n)

JSON/XML/YAML marshalling

Key Types & Functions
type Error

Constructors & wrappers:

New(code codes.Code) *Error

NewWithSlug(code codes.Code, slug string) *Error

Wrap(err error, code codes.Code) *Error

WrapWithSlug(err error, code codes.Code, slug string) *Error

Cast(err error) *Error

Introspection:

(e *Error) Code() codes.Code

(e *Error) GRPCStatus() *status.Status

(e *Error) StatusCode() int (HTTP)

(e *Error) Slug() string

(e *Error) Message() string

(e *Error) Details() any

(e *Error) Validations() any

(e *Error) Localize() bool / SetLocalize(bool)

Example
go
Copy
Edit
func loadThing(id string) error {
  return gerr.NewWithSlug(codes.NotFound, "thing.not_found").
         WithDetailF("id=%s", id)
}
🟦 pkg/s3ext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/s3ext"
What it does
Thin wrapper around S3 providing:

Upload (with optional public URL return)

Download (by key or URL)

Delete

Configs
go
Copy
Edit
type Configs struct {
  S3EndpointURL  url.URL   `env:"S3_ENDPOINT_URL,required"`
  S3AccessKey    string    `env:"S3_ACCESS_KEY,required"`
  S3SecretKey    string    `env:"S3_SECRET_KEY,required"`
  S3Timeout      time.Duration `env:"S3_TIMEOUT" envDefault:"5s"`
  S3MaxRetries   int       `env:"S3_MAX_RETRIES" envDefault:"3"`
  S3BufferSize   int       `env:"S3_BUFFER_SIZE_KB" envDefault:"500"`
  S3BufferGrowth float64   `env:"S3_BUFFER_GROWTH" envDefault:"1.8"`
}
Example
go
Copy
Edit
cfg := s3ext.Configs{
  S3EndpointURL: *mustParseURL("https://s3.example.com"),
  S3AccessKey:   os.Getenv("S3_ACCESS_KEY"),
  S3SecretKey:   os.Getenv("S3_SECRET_KEY"),
}
cli, _ := s3ext.Dial(cfg)

u, _ := cli.Upload("bucket", "path/file.jpg", data, true)
fmt.Println("public URL:", u.String())
🟩 pkg/mapext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/mapext"
Functions
Keys[K comparable, V any](m map[K]V) []K

Values[K comparable, V any](m map[K]V) []V

Merge[K comparable, V any](src, ext map[K]V) map[K]V

Example
go
Copy
Edit
out := mapext.Merge(map[string]int{"a":1}, map[string]int{"b":2})
ks  := mapext.Keys(out)   // ["a","b"]
vs  := mapext.Values(out) // [1,2]
🟨 pkg/templateext
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/templateext"
Function
Format(tmpl string, model any) (string, error)

Example
go
Copy
Edit
msg, _ := templateext.Format("Hello {{.Name}}!", struct{ Name string }{"World"})
// -> "Hello World!"
🟪 pkg/shell
Import:

go
Copy
Edit
import "github.com/pinosell/gopher/pkg/shell"
What it does
Provides helpers for:

Running shell commands

Capturing output and exit codes

Use when you need quick command execution from Go (CI utilities, scaffolding, ops tooling).

🚀 Installation
sh
Copy
Edit
go get github.com/pinosell/gopher@v1.3.16
Import the packages you need:

go
Copy
Edit
import (
  "github.com/pinosell/gopher/pkg/errors"
  "github.com/pinosell/gopher/pkg/s3ext"
  "github.com/pinosell/gopher/pkg/mapext"
  "github.com/pinosell/gopher/pkg/templateext"
  "github.com/pinosell/gopher/pkg/shell"
)
🔗 References
GitHub Repo

pkg.go.dev Documentation