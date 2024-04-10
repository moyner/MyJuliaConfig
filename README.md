# My Julia .config
I recommend the following packages in your base environment: `BenchmarkTools` and `Revise` (run `using Pkg; Pkg.add("BenchmarkTools"); Pkg.add("Revise")`). `Revise` is critical for interactive development, as otherwise updating of code that has already been run will not have any effect. This is my .julia/config/startup.jl file (note the PKG_DEVDIR that you probably want to customize):

```julia
print("Julia with $(Threads.nthreads()) threads: Running custom startup... ")
# Not sure if this matters at the moment
ENV["OPENBLAS_NUM_THREADS"] = 1
using LinearAlgebra
BLAS.set_num_threads(1)
using Revise
# Put dev'd repos somewhere specific instead of `~/.julia/dev`
# Note: You should substitute your own home dir here :)
ENV["JULIA_PKG_DEVDIR"] = "/home/moyner/git"
print("Ok.\n")
``` 

## Skipping precompilation for dev'd packages
It is convenient to skip precompilation if you are actually developing the packages. See [this page for more information](https://julialang.github.io/PrecompileTools.jl/stable/#Package-developers:-reducing-the-cost-of-precompilation-during-development). Here's my setup for `JutulDarcy` that has a long precompilation workload:
```julia
using JutulDarcy, Preferences
set_preferences!(JutulDarcy, "precompile_workload" => false; force=true)
```

# Julia setup
- Julia is most easily installed via [Juliaup](https://github.com/JuliaLang/juliaup) which is planned to be the official version manager. This is available in the Windows store as [Julia published by Julia Computing, Inc](https://github.com/JuliaLang/juliaup). There's also [Jill](https://github.com/abelsiqueira/jill) which makes installing the latest verison of Julia on Linux and setting up the correct paths very quick.
- I use [VSCode](https://code.visualstudio.com/) with the [Julia VSCode extension](https://www.julia-vscode.org/).

## VSCode development setup
The easiest way to have a nice integrated environment when developing a set of related packages is to make a folder somewhere (typically a inside git repo) for the development scripts. Then you can go to File -> Add folder to Workspace and add your `dev` folder. You can then start Julia with Ctrl-shift-p and write Julia: Start REPL to get a Julia session running. Go to the file tree on the left side and right click the folder you are in and select Julia: Activate this environment. You can then enter the Pkg prompt and dev the packages you want to use in this environment:
```julia
] dev Jutul JutulDarcy
```
You can now run scripts interactively, using the default key bindings alt-shift-enter to run a cell (deliminated with ## at the start) or shift-enter to run a line. It is recommended that you save your workspace config under file -> save workspace as so that you can easily restart the workspace when needed. I use one such workspace and environment for each project. Ctrl-T allows you to look up functions and types (highlight the call, then hit ctrl-T to see the options).
