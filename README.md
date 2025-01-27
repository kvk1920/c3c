# C3 Language

C3 is a C-like language trying to be "an incremental improvement over C" rather than a whole new language. 
C3 owes a lot to the ideas of the [C2 language](http://c2lang.org): to iterate on top of C without trying to be a 
whole new language.

C3 tries to be an alternative in the C/C++ niche: fast and close to the metal.

### Design Principles
- Procedural "get things done"-type of language.
- Try to stay close to C - only change what's really necessary.
- C ABI compatibility and excellent C integration.
- Learning C3 should be easy for a C programmer.
- Data is inert.
- Avoid "big ideas" & the "more is better" fallacy.
- Introduce some higher level conveniences where the value is great.

### Example code

Create a `main.c3` file with:
```c++
module hello_world;
import std::io;

func void main()
{
   io::printf("Hello, world!\n");
}
```

Make sure you have the standard libraries at either `../lib/std/` or `/lib/std/`.

Then run
```sh
c3c compile main.c3
```

The generated binary will be called `a.out`.

### In what ways do C3 differ from C?

- No mandatory header files
- New semantic macro system
- Module based name spacing
- Subarrays (slices)
- Compile time reflection
- Enhanced compile time execution
- Generics based on generic modules
- "Result"-based zero overhead error handling
- Defer
- Value methods
- Associated enum data
- Built-in hooks for convenient string handling
- No preprocessor
- Less undefined behaviour and runtime checks in "safe" mode
- Limited operator overloading to enable userland dynamic arrays
- Optional pre and post conditions

### Current status

It's possible to try out the current C3 compiler in the browser: https://ide.judge0.com/ – this is courtesy of the
developer of Judge0. 

Design work is still being done in the design draft here: https://c3lang.github.io/c3docs/. If you have any suggestions, send a mail to [christoffer@aegik.com](mailto:christoffer@aegik.com), [file an issue](https://github.com/c3lang/c3c/issues) or discuss 
C3 on its dedicated Discord: https://discord.gg/qN76R87

The compiler should compile on Linux, Windows (under Mingw or MSYS2) and MacOS, 
but needs some install documentation for Windows. 

Due to its ABI compatibility with C, it's possible to mix C and C3 in the same project.
As a demonstration, vkQuake was compiled with a small portion of the code converted
to C3 and compiled with the c3c compiler:

![vkQuake](https://github.com/c3lang/c3c/blob/master/resources/images/vkQuake.png?raw=true)

(The vkFork is at https://github.com/c3lang/vkQuake)

#### Todo / done

- [x] For/while/do
- [x] `if`/ternary
- [x] Structs
- [x] Union
- [x] Enums
- [x] Value methods
- [x] Compound literals
- [x] Designated initalizers
- [x] Slicing syntax
- [x] Arrays and subarrays
- [x] Modules
- [x] `$unreachable`
- [x] Compile time assert with `$assert`
- [x] Compiler guiding `assert` 
- [x] C code calling by declaring methods `extern`
- [x] Compile time variables
- [x] Basic macros
- [x] 4cc, 8cc, 2cc
- [x] Enum type inference in switch/assignment
- [x] Integer type inference
- [x] Error type
- [x] Failable error handling
- [x] `try` for conditional execution
- [x] `catch` for error handling
- [x] Implicit unwrap after `catch`
- [x] `sizeof`
- [x] `typeof`
- [x] 2s complement wrapping operators
- [x] Labelled break / continue
- [x] `nextcase` statement
- [x] Expression blocks
- [x] Do-without-while
- [x] Foreach statement
- [x] Templates
- [x] Distinct types
- [x] Built-in linking
- [x] CT only macros evaluating to constants
- [x] range initializers e.g. `{ [1..2] = 2 }`
- [x] Trailing body macros e.g. `@foo(1, 100; int a) { bar(a); };`
- [x] Complex macros
- [x] CT type constants
- [ ] Anonymous structs
- [ ] Complete C ABI conformance *in progress*
- [ ] Debug info *in progress*
- [ ] Virtual type *in progress*
- [ ] Enum associated data support  
- [ ] Windows support *in progress*
- [ ] All attributes *in progress*
- [ ] Associative array literals
- [ ] Reflection methods
- [ ] LTO/ThinLTO setup
- [ ] `global` / `shared` for globals 
- [ ] Escape macros
- [ ] Implicit capturing macros
- [ ] Subarray initializers
- [ ] Bitstructs
- [ ] `asm` section
- [ ] `$switch`
- [ ] `$for`
- [ ] Pre-post conditions
- [ ] Stdlib inclusion
- [ ] String functions
- [ ] Simd vector types

#### What can you help with?

- If you wish to contribute with ideas, please file issues on the c3docs: https://github.com/c3lang/c3docs instead of the compiler.
- Discuss the language on discord to help iron out syntax.
- Interested in contributing to the stdlib? Please get in touch on Discord.
- Are you a Windows dev? Please help make the compiler work on Windows!
- Install instructions for other Linux and Unix variants are appreciated.

#### Installing on Ubuntu 20.10

1. Make sure you have a C compiler that handles C11 and a C++ compiler, such as GCC or Clang. Git also needs to be installed.
2. Install CMake: `sudo apt install cmake`
3. Install LLVM 11: `sudo apt-get install clang-11 zlib1g zlib1g-dev libllvm11 llvm-11 llvm-11-dev llvm-11-runtime liblld-11-dev liblld-11`
4. Clone the C3C github repository: `git clone https://github.com/c3lang/c3c.git`
5. Enter the C3C directory `cd c3c`.
6. Create a build directory `mkdir build`
7. Change directory to the build directory `cd build`
8. Set up CMake build for debug: `cmake -DLLVM_DIR=/usr/lib/llvm-11/cmake -DCMAKE_BUILD_TYPE=Debug ..`
9. Build: `cmake --build .`

You should now have a `c3c` executable.

You can try it out by running some sample code: `./c3c compile ../resources/examples/hash.c3`

#### Building via Docker

You can build `c3c` using either an Ubuntu 18.04 or 20.04 container:

```
./build-with-docker.sh 18
```

Replace `18` with `20` to build through Ubuntu 20.04.

For a release build specify:
```
./build-with-docker.sh 20 Release
```

A `c3c` executable will be found under `bin/`.

#### Installing on OS X using Homebrew

2. Install CMake: `brew install cmake`
3. Install LLVM 11: `brew install llvm`
4. Clone the C3C github repository: `git clone https://github.com/c3lang/c3c.git`
5. Enter the C3C directory `cd c3c`.
6. Create a build directory `mkdir build`
7. Change directory to the build directory `cd build`
8. Set up CMake build for debug: `cmake ..`
9. Build: `cmake --build .`
