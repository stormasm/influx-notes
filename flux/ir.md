
In this document:

https://github.com/influxdata/flux/blob/master/docs/CompilationExecution.md

*The initial representation of the query can be either a raw string or an already parsed Abstract Syntax Tree.*

Is the AST generated from a raw Flux String prior to the compilation step ?

### Where in our code is the IR (Intermediate Representation)?

So the IR is what the compiler outputs from your picture in your
document above...

So is the Program the IR ? (see Case I below...)

## Case I

From here we see:

https://github.com/influxdata/flux/blob/master/compiler.go#L14

```
// Compiler produces a specification for the query.
type Compiler interface {
	// Compile produces a specification for the query.
	Compile(ctx context.Context) (Program, error)
	CompilerType() CompilerType
}
```

So in this case the Program which is returned from Compile is the IR ?

## Case II

https://github.com/influxdata/flux/blob/master/examples/library/library_example_test.go#L19

```
ctx, cancelFunc := context.WithCancel(context.Background())
defer cancelFunc()

astPkg := parser.ParseSource(t)
if ast.Check(astPkg) > 0 {
	panic(ast.GetError(astPkg))
}
compiler := lang.ASTCompiler{
	AST: astPkg,
}

program, err := compiler.Compile(ctx)
if err != nil {
	panic(err)
}

ctx = executetest.NewTestExecuteDependencies().Inject(ctx)
alloc := &memory.Allocator{}
q, err := program.Start(ctx, alloc)
if err != nil {
	panic(err)
}
```

The program the IR ??

## Case III

https://github.com/influxdata/flux/blob/master/lang/compiler_test.go#L320

```
  program, err := lang.Compile(src, now, opt)
  if err != nil {
    t.Fatalf("failed to compile script: %v", err)
  }

  // start program in order to evaluate planner options
  ctx := executetest.NewTestExecuteDependencies().Inject(context.Background())
	if _, err := program.Start(ctx, &memory.Allocator{}); err != nil {
		t.Fatalf("failed to start program: %v", err)
	}
```

References:

[Wasmtime](https://github.com/bytecodealliance/wasmtime)

[Cranelift IR Reference](https://github.com/bytecodealliance/wasmtime/blob/master/cranelift/docs/ir.md)

[Hackernews Post: A possible new backend for Rust](https://news.ycombinator.com/item?id=22934848)

https://jason-williams.co.uk/a-possible-new-backend-for-rust

Here are some notes from the reference above:

##### Note 1

*You can scan through your source code, parse it into an Abstract Syntax Tree (AST) then generate some abstract language (let’s call this Intermediate Representation) which LLVM can understand, LLVM says “Thanks! We’ll take it from here”.*

##### Note 2

*In Rust, rustc is the main compiler which your source code is fed into first, it does things a typical compiler would do like generate an AST (in this context we call a High-Level Representation, or HIR for short). Once in tree-form type checking and other tasks can be performed then it’s compiled down to another representation ready for whichever backend takes it. The default backend of rustc is called rustc_codegen_llvm2 (or cg_llvm) which itself also acts as a front end to LLVM.*
