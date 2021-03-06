lug
===
An embedded domain specific language for expressing parsers as extended [parsing expression grammars (PEGs)](https://en.wikipedia.org/wiki/Parsing_expression_grammar) in C++17

Features
---
- Natural syntax more akin to external parser generator languages, unlike many other C++ parsing toolkits
- Direct and indirect left recursion with precedence levels to disambiguate subexpressions with mixed left/right recursion
- Traditional PEG syntax has been extended to support attribute grammars
- Cut operator to commit to currently matched parse prefix and prune all backtrack entries
- Generated parsers are compiled down to special-purpose bytecode and executed in a virtual parsing machine
- Uses expression template functors to implement the rules of the domain specific language
- UTF-8 text parsing with support for matching Unicode character classes
- Single header only library using C++17 language and library features
- Relatively small with the intent to remain under 1000 lines of very terse code

It is based on research introduced in the following papers:

> Bryan Ford, [Parsing expression grammars: a recognition-based syntactic foundation](https://doi.org/10.1145/982962.964011), Proceedings of the 31st ACM SIGPLAN-SIGACT symposium on Principles of Programming Languages, p.111-122, January 2004

> Sérgio Medeiros et. al, [A parsing machine for PEGs](https://doi.org/10.1145/1408681.1408683), Proceedings of the 2008 symposium on Dynamic Languages, p.1-12, July 2008

> Kota Mizushima et. al, [Packrat parsers can handle practical grammars in mostly constant space](https://doi.org/10.1145/1806672.1806679), Proceedings of the 9th ACM SIGPLAN-SIGSOFT workshop on Program analysis for software tools and engineering, p.29-36, June 2010

> Sérgio Medeiros et. al, [Left recursion in Parsing Expression Grammars](https://doi.org/10.1016/j.scico.2014.01.013), Science of Computer Programming, v.96 n.P2, p.177-190, December 2014

> Leonardo Reis et. al, [The formalization and implementation of Adaptable Parsing Expression Grammars](https://doi.org/10.1016/j.scico.2014.02.020), Science of Computer Programming, v.96 n.P2, p.191-210, December 2014

> Sérgio Medeiros et. al, [A parsing machine for parsing expression grammars with labeled failures](https://doi.org/10.1145/2851613.2851750), Proceedings of the 31st Annual ACM symposium on Applied Computing, p.1960-1967, April 2016

Building
---
As a header only library, lug itself does not need to be built.
Just drop in the single `lug.hpp` header file into a directory that is in your header include path and you're good to go.

As a baseline, the following compiler versions are known to work with lug.

| Compiler | Language Mode |
| --- | --- |
| Clang 4.0.0 (February 2017) | -std=c++1z or -std=gnu++1z (Must use libstdc++ 7.1 as standard library. As of July 2017, libc++ does not implement the is_invokable suite of type traits required by lug.) |
| GCC 7.1.0 (May 2017) | -std=c++17 or -std=gnu++17 |
| Microsoft Visual C++ 2017 15.3 Preview 2 (June 2017) | Platform Toolset: Visual Studio 2017 Toolset (v141), Language Standard: ISO C++17 Standard (/std:c++17) |

For building the sample programs and unit tests, a makefile is provided for Linux and BSD platforms and a Visual Studio solution is available for use on Windows.

TODO
---
- parser error recovery
- add an interactive processing mode flag to input sources?
- handle exceptions thrown from semantic actions in semantics::accept?
- feature: symbol tables and parsing conditions
- feature: Adams' grammars and alignment elimination
- feature: syntax to specify number range of allowed iteration
- optimization: better detection of left-recursive rule calls to remove false-positives
- optimization: tail recursion
- optimization: additional instructions
- more samples, testing, and bug fixing
- increase compiler warning level and fix any issues
- documentation