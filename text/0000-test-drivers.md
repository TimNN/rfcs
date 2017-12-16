- Feature Name: test_drivers
- Start Date: 2017-12-13
- RFC PR:
- Rust Issue:

# Summary
[summary]: #summary

Rust currently provides basic unit testing support and unstable benchmarking support. However there is desire for benchmarking support on stable and more advanced test features, such as parameterized tests or "tear down" and "setup" functions. Keeping in mind Rust's goal of providing a small set of core functionality, none of these features seem to have a place in the standard rust distribution, but should be provided by external crates. This RFC proposes a (hopefully) lightweight API for `libtest`, allowing all these use cases, and more, to be supported by external crates.

# Motivation
[motivation]: #motivation

The goal of this RFC is for external crates to be able to implement all of the following features in a composable manner, while seamlessly integrating with the `#[test]` attribute:

1. **Parameterized tests**: Certain tests benefit from being run over a range of parameters, for example all values of a (C-like) enum.
1. **Dynamic test case generation**: Sometimes tests benefit from being defined in some "external" source, for example when using `compile-test`, each file in a certain directory represents one test case. It should be possible to dynamically determine the list of tests to run during test initialization.
1. **Benchmarking**: Benchmarking is currently implemented as an unstable feature of `libtest`. However following Rust's principle of keeping a lean standard library, this seems like a feature which could much better be provided externally.
1. **Advanced test life cycle**: Especially in integration test scenarios it may be beneficial to have some shared "setup" or "tearDown" code which is run before / after either each tests or all tests.
1. **Modify test behavior**: It should be possible to add "rules" which modify test success / failure conditions, for example rules could:
    * Add a special kind of "non-aborting assertions", i.e. assertions which while cause the entire test to fail but do not abort its execution when they are triggered.
    * Allow making assertions about log messages, e.g. "there may be no log statements above `info`, except the following ones".
    * Mark tests as ignored / skipped if certain conditions are not met at runtime.

## Other Requirements
[other-requirements]: #other-requirements

Apart from providing a solution for the above use cases, the following requirements should be met:

1. The solution should allow composing different features, for example it should be possible to have parameterized benchmarks.
1. The existing unit test functionality must still be supported out-of-the-box.
1. Wherever possible, all APIs in `libtest` should be future-proof, i.e. extendable without breaking changes.

# Guide-level explanation
[guide-level-explanation]: #guide-level-explanation

**TODO**

<!-- Explain the proposal as if it was already included in the language and you were teaching it to another Rust programmer. That generally means:

- Introducing new named concepts.
- Explaining the feature largely in terms of examples.
- Explaining how Rust programmers should *think* about the feature, and how it should impact the way they use Rust. It should explain the impact as concretely as possible.
- If applicable, provide sample error messages, deprecation warnings, or migration guidance.
- If applicable, describe the differences between teaching this to existing Rust programmers and new Rust programmers.

For implementation-oriented RFCs (e.g. for compiler internals), this section should focus on how compiler contributors should think about the change, and give examples of its concrete impact. For policy RFCs, this section should provide an example-driven introduction to the policy, and explain its impact in concrete terms. -->

# Reference-level explanation
[reference-level-explanation]: #reference-level-explanation

**TODO**

<!-- This is the technical portion of the RFC. Explain the design in sufficient detail that:

- Its interaction with other features is clear.
- It is reasonably clear how the feature would be implemented.
- Corner cases are dissected by example.

The section should return to the examples given in the previous section, and explain more fully how the detailed proposal makes those examples work. -->

# Drawbacks
[drawbacks]: #drawbacks

**TODO**

<!-- Why should we *not* do this? -->

# Rationale and alternatives
[alternatives]: #alternatives

**TODO**

<!-- - Why is this design the best in the space of possible designs?
- What other designs have been considered and what is the rationale for not choosing them?
- What is the impact of not doing this? -->

# Unresolved questions
[unresolved]: #unresolved-questions

**TODO**

<!-- - What parts of the design do you expect to resolve through the RFC process before this gets merged?
- What parts of the design do you expect to resolve through the implementation of this feature before stabilization?
- What related issues do you consider out of scope for this RFC that could be addressed in the future independently of the solution that comes out of this RFC? -->
