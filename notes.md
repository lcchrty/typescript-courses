# enterprise typescript course

## intro

Enterprise software just means software intended for large organizations. How large? For the purposes of this course, let’s say big enough that

    No one person could possibly master the entire codebase
    Multiple teams are involved in the evolution of the project, and they don’t want to be tightly coupled with each other
    If everyone “does their own thing” the codebase (and resultant product) will lose cohesion and become unmanageable

**Productivity**. A broken build, an incompatible dependency, etc… interrupts the work of many people.
A **balance** opinionated foundations, and flexibility. There need to be helpful forces that keep the project cohesive, while still providing enough flexibility for creative license, and customizations to meet certain needs in specific areas of the codebase.
Designing for a **long shelf life**. Successful large projects are often around for a long time. They need to be able to evolve as things change, and avoid the need for a rewrite every few years
Managing **complexity**. Once a codebase gets large enough, managing the interactions between different areas starts to become overwhelming if the architecture is not designed well.

## goals

1. We’ll create a TypeScript library from scratch, with API docs, linting and automated detection of changes to our public API surface!
2. We’ll migrate a non-trivial JS codebase to TypeScript, using a low-risk predictable and incremental strategy
3. We’ll look at how to keep pace with new TS compiler versions and deal with breaking changes using rehearsal-js typesVersions and downlevel-dts
4. We’ll develop an in-depth understanding of “strictness”

> install YARN in course repo
