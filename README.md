# atreugo-swagger
[![codebeat badge](https://codebeat.co/badges/103ada91-026a-4027-b450-1a0ccbf8ce9a)](https://codebeat.co/projects/github-com-nerzal-atreugo-swagger-master)
[![Go Report Card](https://goreportcard.com/badge/github.com/Nerzal/atreugo-swagger)](https://goreportcard.com/report/github.com/Nerzal/atreugo-swagger)
[![Go Doc](https://godoc.org/github.com/Nerzal/atreugo-swagger?status.svg)](https://godoc.org/github.com/Nerzal/atreugo-swagger)
[![Build Status](https://github.com/Nerzal/atreugo-swagger/workflows/Tests/badge.svg)](https://github.com/Nerzal/atreugo-swagger/actions?query=branch%3Amaster+event%3Apush)
[![GitHub release](https://img.shields.io/github/tag/Nerzal/atreugo-swagger.svg)](https://GitHub.com/Nerzal/atreugo-swagger/releases/)
[![codecov](https://codecov.io/gh/Nerzal/atreugo-swagger/branch/master/graph/badge.svg)](https://codecov.io/gh/Nerzal/atreugo-swagger)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FNerzal%2Fatreugo-swagger.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FNerzal%2Fatreugo-swagger?ref=badge_shield)

atreugo handler that serves swagger files. 

Works with [swaggo](https://github.com/swaggo/swag)

swagger files are from: [swaggofiles](https://github.com/swaggo/files)

## Paths
Serves swagger documentation under index.html

Serves redoc documentation under redoc.html

## Example


```go
package main

import (
	atreugoswagger "github.com/Nerzal/atreugo-swagger"
	_ "github.com/Nerzal/atreugo-swagger/example/docs" // docs is generated by Swag CLI, you have to import it.
	"github.com/savsgio/atreugo/v10"
)

// @title Swagger Example API
// @version 1.0
// @description This is a sample server Petstore server.
// @termsOfService http://swagger.io/terms/

// @contact.name API Support
// @contact.url http://www.swagger.io/support
// @contact.email support@swagger.io

// @license.name Apache 2.0
// @license.url http://www.apache.org/licenses/LICENSE-2.0.html

// @host petstore.swagger.io
// @BasePath /v2
func main() {
	config := &atreugo.Config{
		Addr: "0.0.0.0:1337",
	}

	a := atreugo.New(config)

	// This will server all swagger files under the /docs/* path.
	a.GET("/docs/*doc", atreugoswagger.AtreugoWrapHandler(atreugoswagger.Title("Test Title")))

	// Start the server
	err := a.ListenAndServe()
	if err != nil {
		panic(err)
	}
}

```
