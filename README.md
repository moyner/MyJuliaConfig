# My Julia .config
I recommend the following packages in your base environment: `AbbreviatedStackTraces` (+`Suppressor` for loading), `BenchmarkTools` and `Revise`. `Revise` is critical for interactive development, as otherwise updating of code that has already been run will not have any effect. This is my .julia/config/startup.jl file:

```julia
print("Julia with $(Threads.nthreads()) threads: Running custom startup... ")
# For abbreviated stack traces, loaded later
ENV["JULIA_STACKTRACE_MINIMAL"] = true
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
using Revise
print("Ok.\n")
# Put dev'd repos somewhere specific instaed of `./julia/dev`
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
# Trick to get abbreviated stack traces loaded inside VSCode
@async begin
    sleep(3)
    @eval using Suppressor
    @eval @suppress using AbbreviatedStackTraces
end
print("Ok.\n")
``` 
# Julia setup
- Julia is most easily installed via [Juliaup](https://github.com/JuliaLang/juliaup) which is planned to be the official version manager. This is available in the Windows store as [Julia published by Julia Computing, Inc](https://github.com/JuliaLang/juliaup). There's also [Jill](https://github.com/abelsiqueira/jill) which makes installing the latest verison of Julia on Linux and setting up the correct paths very quick.
- I use [VSCode](https://code.visualstudio.com/) with the [Julia VSCode extension](https://www.julia-vscode.org/).
