### What is an Operation Spec ?

[Definition of Spec](https://github.com/influxdata/flux/blob/master/spec.go)

```go
// Spec specifies a query.
type Spec struct {
	Operations []*Operation       `json:"operations"`
	Edges      []Edge             `json:"edges"`
	Resources  ResourceManagement `json:"resources"`
	Now        time.Time          `json:"now"`

	sorted   []*Operation
	children map[OperationID][]*Operation
	parents  map[OperationID][]*Operation
}
```

These specs are defined in the corresponding individual files located in
[stdlib/universe](https://github.com/influxdata/flux/tree/master/stdlib/universe)

```go
type CountOpSpec struct {
	execute.AggregateConfig
}

type CumulativeSumOpSpec struct {
	Columns []string `json:"columns"`
}

type DifferenceOpSpec struct {
	NonNegative bool     `json:"nonNegative"`
	Columns     []string `json:"columns"`
}

type DistinctOpSpec struct {
	Column string `json:"column"`
}

type FilterOpSpec struct {
	Fn *semantic.FunctionExpression `json:"fn"`
}

type FirstOpSpec struct {
	execute.SelectorConfig
}

type GroupOpSpec struct {
	Mode    string   `json:"mode"`
	Columns []string `json:"columns"`
}

type HistogramOpSpec struct {
	Column           string    `json:"column"`
	UpperBoundColumn string    `json:"upperBoundColumn"`
	CountColumn      string    `json:"countColumn"`
	Bins             []float64 `json:"bins"`
	Normalize        bool      `json:"normalize"`
}

type MapOpSpec struct {
	Fn       *semantic.FunctionExpression `json:"fn"`
	MergeKey bool                         `json:"mergeKey"`
}

type MeanOpSpec struct {
	execute.AggregateConfig
}

type MinOpSpec struct {
	execute.SelectorConfig
}

type MovingAverageOpSpec struct {
	N       int64    `json:"n"`
	Columns []string `json:"columns"`
}

type RangeOpSpec struct {
	Start       flux.Time `json:"start"`
	Stop        flux.Time `json:"stop"`
	TimeColumn  string    `json:"timeColumn"`
	StartColumn string    `json:"startColumn"`
	StopColumn  string    `json:"stopColumn"`
}

type SetOpSpec struct {
	Key   string `json:"key"`
	Value string `json:"value"`
}

type SortOpSpec struct {
	Columns []string `json:"columns"`
	Desc    bool     `json:"desc"`
}

type SumOpSpec struct {
	execute.AggregateConfig
}

type UniqueOpSpec struct {
	Column string `json:"column"`
}

type WindowOpSpec struct {
	Every       flux.Duration `json:"every"`
	Period      flux.Duration `json:"period"`
	Offset      flux.Duration `json:"offset"`
	TimeColumn  string        `json:"timeColumn"`
	StopColumn  string        `json:"stopColumn"`
	StartColumn string        `json:"startColumn"`
	CreateEmpty bool          `json:"createEmpty"`
}

type YieldOpSpec struct {
	Name string `json:"name"`
}
```
