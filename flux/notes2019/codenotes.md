
in package lang
there is a file compiler.go
which has most of the core high level logic.
see the method Start for the toplevel stuff.
I guess eventually this will be replaced
by the new work affo is working on
(see references below to CompilationExecution)

these 2 lines of code seems pretty mission critical
to understanding what happens to the results

```
	e := execute.NewExecutor(p.Dependencies, p.Logger)
```

```
	go p.processResults(ctx, q, resultMap)
```

so this is going to be a random stream of consciousness
but eventually this will get organized and make more sense

here are some key lines of code that I am working on that
will hopefully tie things together

in package repl
there is a method doQuery
[which has a line of code](https://github.com/influxdata/flux/blob/master/repl/repl.go#L183)

```
results, err := r.querier.Query(ctx, replCompiler)
```

For now assume that this part is a black box and I will
focus on what happens after this to the **results**.

#### References

[CompilationExecution](https://github.com/influxdata/flux/blob/f99d37e446e8b18aed9be0835e724f3e3215c657/docs/CompilationExecution.md)
