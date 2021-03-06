[![GoDoc](https://godoc.org/github.com/romanyx/polluter?status.svg)](https://godoc.org/github.com/romanyx/polluter)
[![Go Report Card](https://goreportcard.com/badge/github.com/romanyx/polluter)](https://goreportcard.com/report/github.com/romanyx/polluter)

# polluter

Mainly this package was created for testing purposes, to give the ability to seed a database with records from simple .yaml files.

## Usage

```go
package main

import "github.com/romanyx/polluter"

const input = `
users:
- id: 1
  name: Roman
`

func TestX(t *testing.T) {
	db := prepareMySQL(t)
	defer db.Close()
	p := polluter.New(polluter.MySQLEngine(db))

	if err := p.Pollute(strings.NewReader(input)); err != nil {
		t.Fatalf("failed to pollute: %s", err)
	}

	....
}
```

## Examples

[See](https://github.com/romanyx/polluter/blob/master/polluter_test.go#L109) examples of usage with the single transaction sql driver for parallel testing.

## Testing

Make shure to start docker before testing.

```bash
make start
go test
```

## Supported databases

* MySQL
* Postgres

## Contributing

Please feel free to submit issues, fork the repository and send pull requests!

## TODO

* [ ] SQLite support
* [ ] MongoDB support
* [ ] Other DB's support
* [ ] Input validation for better errors
* [ ] JSON unmarshal algorithm improvement
