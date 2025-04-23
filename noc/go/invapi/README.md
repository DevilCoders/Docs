INVAPI example.

```go
package main

import (
	"context"
	"fmt"

	"github.com/hasura/go-graphql-client"
	"gopkg.in/yaml.v2"

	"a.yandex-team.ru/library/go/core/log"
	"a.yandex-team.ru/library/go/core/log/zap"
	"a.yandex-team.ru/noc/go/invapi"
)

type Tag struct {
	Tag string
}

type Alloc struct {
	IP  string
	Net struct {
		ETags []Tag `graphql:"etags"`
		ITags []Tag `graphql:"itags"`
	}
}

type Device struct {
	Name     string
	FQDN     string
	DC       string
	ETags    []Tag `graphql:"etags"`
	ITags    []Tag `graphql:"itags"`
	Allocs   []Alloc
	Hardware struct {
		Model  string
		Type   string
		Vendor string
	}
	Soft struct {
		Name    string
		Type    string
		Version string
	}
}

func getHosts(ctx context.Context, config *invapi.Config, rackCode string, logger log.Logger) ([]Device, error) {
	logger = logger.WithName("invapi")

	var query struct {
		Object []Device `graphql:"object(code: $rackcode)"`
	}
	variables := map[string]interface{}{"rackcode": graphql.String(rackCode)}

	conn, err := invapi.NewClient(ctx, config, logger.WithName("invapi"))
	err = conn.Query(ctx, &query, variables)
	if err != nil {
		logger.Error("GraphQL request failed", log.Error(err))
		return nil, err
	}

	return query.Object, nil
}

func main() {
	defaultLogger := zap.Must(zap.StandardConfig("console", log.DebugLevel))
	yamlFile := `
oauth: "TOKE-N"
url: "https://ro.racktables.yandex-team.ru/api"
`
	c := &invapi.Config{
		URL:   "",
		OAuth: nil,
	}
	err := yaml.Unmarshal([]byte(yamlFile), c)
	if err != nil {
		panic(err)
	}
	ctx := context.Background()
	hosts, err := getHosts(ctx, c, "{$cn_noc-sas}", defaultLogger)
	if err != nil {
		panic(err)
	}
	fmt.Printf("%v\n", hosts)
}
```
