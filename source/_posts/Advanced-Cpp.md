# C/C++ Advanced StudyNote

## Project Structure

A C/C++ Project should be like as follows:

```mermaid

Graph LR;

A[root] -> B[debug]
A -> C[release]
A -> D[dist]
A -> E[docs]
A -> F[include]
A -> G[lib]
A -> H[src]
A -> I<samples>
A -> J<test>
A -> K(README)
A -> L[Makefile/cmake]
A -> M(LICENSE)
A -> N(CMakeList.txt)
A -> O(.gitignore)
A -> P(.travis.yml)
A -> Q<Docker>
A -> R[scripts]
A -> S[some modules]
```

## Documenting

### Interface & Function

- `@brief <discription>`: A brief discription of Function.

- `@param <parameter> <discription>`: Discription for each parameter(if have, multi-lines when multi-parameters).

- `@return <discription>`: Discription for the return value(if have).



