# My Julia .config
I recommend the following packages in your base environment: `BenchmarkTools` and `Revise` (run `using Pkg; Pkg.add("BenchmarkTools"); Pkg.add("Revise")`). `Revise` is critical for interactive development, as otherwise updating of code that has already been run will not have any effect. This is my .julia/config/startup.jl file (note the PKG_DEVDIR that you probably want to customize):

```julia
print("Julia with $(Threads.nthreads()) threads: Running custom startup... ")
# Not sure if this matters at the moment
ENV["OPENBLAS_NUM_THREADS"] = 1
using LinearAlgebra
BLAS.set_num_threads(1)
using Revise
# Put dev'd repos somewhere specific instead of `./julia/dev`
# Note: You should substitute your own home dir here :)
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
print("Ok.\n")
``` 
## Shorter stack traces
You can also add  [`AbbreviatedStackTraces`](https://github.com/BioTurboNick/AbbreviatedStackTraces.jl) (+`Suppressor` for loading) to the base environment and add the following to your startup file:
```julia
# For abbreviated stack traces, loaded later
ENV["JULIA_STACKTRACE_MINIMAL"] = true
# Trick to get abbreviated stack traces loaded inside VSCode
@async begin
    sleep(3)
    @eval using Suppressor
    @eval @suppress using AbbreviatedStackTraces
end
```

## Skipping precompilation for dev'd packages
It is convenient to skip precompilation if you are actually developing the packages. Here's my setup:
```julia
using SnoopPrecompile, Preferences
set_preferences!(SnoopPrecompile, "skip_precompile" => ["Jutul", "JutulDarcy"])
```

# Julia setup
- Julia is most easily installed via [Juliaup](https://github.com/JuliaLang/juliaup) which is planned to be the official version manager. This is available in the Windows store as [Julia published by Julia Computing, Inc](https://github.com/JuliaLang/juliaup). There's also [Jill](https://github.com/abelsiqueira/jill) which makes installing the latest verison of Julia on Linux and setting up the correct paths very quick.
- I use [VSCode](https://code.visualstudio.com/) with the [Julia VSCode extension](https://www.julia-vscode.org/).
