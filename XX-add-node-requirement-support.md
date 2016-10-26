# Add Node Requirement Support

Phil Myers, 10-26-2016

## Introduction
This proposal suggests adding support for Node Requirement (`depends_on :node`) to the Formula DSL.

## Motivation
The Formula DSL currently requires the `node` dependency to be installed via `brew`. There are many ways to install `node`. Implementing this proposal would allow users who installed `node` without using `brew` to not have to unnecessarily re-install `node` using `brew` for formulas with `node` dependencies.

An issue that would be solved by adding support for `depends_on :node` exists [here](https://github.com/Homebrew/homebrew-core/issues/6187). I had the same problem. Mike McQuaid suggested this solution.

## Proposed solution
* Create a `NodeRequirement` class
* Add `depends_on :node` to the Formula DSL
* Update `Node-for-Formula-Authors.md` to suggest using `depends_on :node` instead of `depends_on "node"`

## Detailed design
* Use any of the files in `brew/Library/Homebrew/requirements` as a template for writing the `NodeRequirement` class
* Similarly to the other requirements, fallback to using `brew` to install `node` via `default_formula` if it doesn't exist. This maintains backwards compatibility.
* Update `DependencyCollector#parse_symbol_spec` to look for `:node`

## Alternatives considered
The `Requirement` pattern seems fairly straightforward; I can't think of any alternatives.
