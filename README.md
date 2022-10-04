# MyJuliaConfig
I recommend the following packages in your base environment: `AbbreviatedStackTraces, BenchmarkTools` and `Revise`. Revise is critical for active development.

```julia
print("Running custom startup... ")
# For abbreviated stack traces, loaded later
ENV["JULIA_STACKTRACE_MINIMAL"] = true
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
using Revise
print("Ok.\n")
``` 
