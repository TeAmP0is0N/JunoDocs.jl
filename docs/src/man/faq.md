# FAQ

### I am having issues, where do I leave a bug report?

Please leave bug reports either
on [Juno.jl GitHub repository](https://github.com/JunoLab/Juno.jl/issues) or
at [Julia Discourse under the `Tooling ▶ Juno` category](https://discourse.julialang.org/c/tools/juno/l/latest).

!!! note
    When you report a problem, please add the output of `Julia Client: Debug Info` command or `Juno > Debug Information` menus entry if possible.

### Juno could not be started.

Go to `Packages > Juno > Settings` and change `Julia Path` to point to the Julia binary.

### I have issues on update !

Please follow the steps described in [Update Instructions](@ref).

### Juno doesn't work properly after an Atom update. What do I do?

Check whether you have a little red bug symbol in the status bar (lower right):

![native bug](../assets/native_bug.png)

If so, click on it and then click on `Rebuild Packages`:

![native update](../assets/native_update.png)

Restart Atom and you should be good to go!

### The integrated REPL/terminal is unbearably slow. How do I fix it?

Enable the `Fallback Renderer` option in the `Terminal Options` in julia-client's settings
and restart Atom for good measure.

### Some Juno package is using the wrong precompile cache, what do I do?

This problem manifests itself in errors like:

```julia
WARNING: Method definition
WARNING: Module Juno with uuid 738353145462472 is missing from the cache.
ERROR: LoadError: Declaring precompile(false) is not allowed in files that are being precompiled.
ERROR: LoadError: Failed to precompile Atom to C:\Users...
```

One way this can occur is from updating Julia versions. However, this has a very
easy fix. Go into the Julia REPL (not the Juno console in Atom, but the actual
Julia terminal window) and type in the command:

```julia
using Atom
```

That will force Julia to re-compile all of the cache files and should fix the problem.

### I am having a problem running Juno with an older version of Julia, why?

Juno is under rapid development, so it's expected that previous versions may not
be compatible with the Atom packages overtime. Julia will automatically use older
versions on the Julia-side packages, but Atom will always give you the most up-to-date
packages it knows about, which causes this issue. The easy way to solve this is
to always use the current Julia release. Otherwise, resort to the [Developer Installation Instructions](@ref)
for the Atom packages and use git to checkout an older version. This requires some
git know-how, so it's only recommended if the older version of Julia is truly necessary.

### How do I use Juno with the Julia Nightly version?

If you want to use Juno with the nightly version use caution: this package is under
rapid development so do so at your own risk. That being said, the Julia nightly
should work using the [Developer Installation Instructions](@ref). Note that this will require you to
be on master for the Julia and Atom packages, so things will be changing likely
before documentation changes.

### How do I execute code on Juno startup?

Much like Julia has its `~/.julia/config/startup.jl` file for executing code on startup, Juno will execute code contained in `~/.julia/config/juno_startup.jl` after Julia has been booted and a connection with the editor is established. This allows running code on startup that queries the frontend, e.g. [`Juno.syntaxcolors`](@ref).

### How do I enable code autocompletion?

Autocompletion is already active, but Juno needs an attached Julia session to
fetch the function, struct and such definitions. A julia process can be started
using the sidebar ("Start local julia process" option) or using the keyboard
shortcut (`Ctrl-J Ctrl-S` by default). Following the same logic, autocompletions
will be available for packages other than `Base` and `Core` only if they are
loaded into the julia process. This can be achieved by executing the code in
your source file using a shortcut like `Ctrl-Enter`. For example, executing
`using LinearAlgebra` will enable autocompletions for the LinearAlgebra package.

### What do I do about `/lib64/libstdc++.so.6: version 'CXXABI_1.3.9' not found` issues on older Linux versions?

If you cannot update your libstdc++ (or Linux distro) then you can use the libstdc++ shipped with Julia 
instead by running
```
export LD_PRELOAD=${JULIA_INSTALL}/lib/julia/libstdc++.so.6
```
before starting Atom.

