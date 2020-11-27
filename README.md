# echo-swagger

echo v3 middleware to automatically generate RESTful API documentation with Swagger 2.0.


## Usage

### Start using it
1. Add comments to your API source code, [See Declarative Comments Format](https://github.com/swaggo/swag#declarative-comments-format).
2. Download [Swag](https://github.com/swaggo/swag) for Go by using:
```sh
$ go get github.com/swaggo/swag/cmd/swag
```
3. Run the [Swag](https://github.com/swaggo/swag) in your Go project root folder which contains `main.go` file, [Swag](https://github.com/swaggo/swag) will parse comments and generate required files(`docs` folder and `docs/doc.go`).
```sh_ "github.com/zestmoney/echo-swagger/v2/example/docs"
$ swag init
```
4. Download [echo-swagger](https://github.com/zestmoney/echo-swagger) by using:
```sh
$ go get -u github.com/zestmoney/echo-swagger@1.0.2
```

And import following in your code:
```go
import "github.com/zestmoney/echo-swagger" // echo-swagger middleware
```

### Canonical example:

```go
package main

import (
	"github.com/labstack/echo"
	"github.com/zestmoney/echo-swagger"

	_ "github.com/zestmoney/echo-swagger/example/docs" // docs is generated by Swag CLI, you have to import it.
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
	e := echo.New()

	e.GET("/swagger/*", echoSwagger.WrapHandler)

	e.Logger.Fatal(e.Start(":1323"))
}

```

5. Run it, and browser to http://localhost:1323/swagger/index.html, you can see Swagger 2.0 Api documents.

![swagger_index.html](https://user-images.githubusercontent.com/8943871/36250587-40834072-1279-11e8-8bb7-02a2e2fdd7a7.png)

