Siberia Env
=================

[![Author](https://img.shields.io/badge/author-@nao99-green.svg)](https://github.com/nao99)
[![Source Code](https://img.shields.io/badge/source-siberia_env/main-blue.svg)](https://github.com/nao99/siberia-projects/tree/main/siberia-env)

## What is it?
Siberia-env is a library written on clear go for working with environment variables

For now the library provides a method to expand all labeled (${ENV_VARIABLE_NAME})
environment variables in a content to their real values

## How to download?

```console
john@doe-pc:~$ go get github.com/nao99/siberia-projects/siberia-env
```

## How to use?
 - Label places you want to expand in your content with "${}" symbols sequence
 - Provide a name of a variable a value of which you want to extract
 - (Optional) Provide a default value using ":" symbol (could be empty)
 - Call the "env.ExpandEnvIn" method with the content

## Examples
```yaml
my:
  custom:
    properties:
      headers:
        - key: Cache-Control
          value: ${CACHE_CONTROL:no-cache}
        - key: Content-Type
          value: application/json
```

```go
    package main

    import (
		"github.com/nao99/siberia-projects/siberia-env/pkg/env"
		"io"
		"os"
    )

    func main() {
		file, _ := os.Open("path_to_the_yaml_file_above.yaml")
		defer file.Close()

		fileContent, _ := io.ReadAll(file)

		expandedFileContent, _ := env.ExpandEnvIn(fileContent)
		expandedFileContentString := string(expandedFileContent)
		
		println(expandedFileContentString)
    }
```

```console
my:
  custom:
    properties:
      headers:
        - key: Cache-Control
          value: no-cache
        - key: Content-Type
          value: application/json
```
