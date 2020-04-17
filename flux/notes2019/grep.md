
##### grh "\.Start(" *

```
cmd/flux/cmd/repl.go:	qry, err := program.Start(ctx, alloc)

examples/library/library_example_test.go:	q, err := program.Start(ctx, alloc)

internal/cmd/refactortests/cmd/refactortests.go:	q, err := program.Start(context.Background(), alloc)

lang/compiler.go:	return p.Program.Start(ctx, alloc)
lang/query_test.go:	q, err := program.Start(context.Background(), &memory.Allocator{})
lang/compiler_test.go:			if _, err = program.Start(context.Background(), &memory.Allocator{}); tc.err == "" && err != nil {
lang/compiler_test.go:	_, err = program.Start(context.Background(), &memory.Allocator{})
lang/compiler_test.go:			if _, err := program.Start(context.Background(), &memory.Allocator{}); err != nil {
lang/compiler_test.go:	if _, err := program.Start(context.Background(), &memory.Allocator{}); err != nil {
lang/compiler_test.go:	q, err := program.Start(context.Background(), &memory.Allocator{})

querytest/execute.go:	query, err := program.Start(ctx, alloc)

stdlib/universe/table_fns.go:	q, err := p.Start(context.Background(), &memory.Allocator{})
stdlib/flux_test.go:	r, err := program.Start(context.Background(), alloc)
stdlib/flux_test.go:	r, err := program.Start(context.Background(), alloc)
```
