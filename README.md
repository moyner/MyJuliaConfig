# MyJuliaConfig
I recommend the following packages in your base environment: `AbbreviatedStackTraces` (+`Suppressor` for loading), `BenchmarkTools` and `Revise`. Revise is critical for active development. This is my .julia/config/startup.jl file:

```julia
print("Julia with $(Threads.nthreads()) threads: Running custom startup... ")
# For abbreviated stack traces, loaded later
ENV["JULIA_STACKTRACE_MINIMAL"] = true
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
using Revise
print("Ok.\n")
# using AbbreviatedStackTraces
ENV["JULIA_STACKTRACE_MINIMAL"] = true
# Put dev'd repos somewhere specific
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
@async begin
    sleep(3)
    @eval using Suppressor
    @eval @suppress using AbbreviatedStackTraces
end
print("Ok.\n")
``` 
