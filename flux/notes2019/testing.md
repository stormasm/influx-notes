
#### How to test the Flux code base

To run individual tests change the top level Makefile

```
export GO_TEST=env GO111MODULE=on go test $(GO_ARGS)
export GO_TEST=env GO111MODULE=on go test -count=1 -v -run TestSort $(GO_ARGS)

$(GO_TEST) $(GO_TEST_FLAGS) ./...
$(GO_TEST) $(GO_TEST_FLAGS) ./stdlib/universe

```
