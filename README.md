# The heavy-traffic diffusion limit of symmetric queues

Yitzchak Shmalo

This repository contains the paper and the computations for the following result. Consider an M/G/1 queue under a symmetric service discipline in Kelly's sense: at queue length n the job in position i receives the fraction gamma(n,i) of the server, and an arriving job joins position i with probability gamma(n+1,i). Let the service requirement B satisfy E B^2 < infinity, let r(1 - lambda_r E B) tend to beta, and start the queue empty. Then for every symmetric discipline

    Q_r(r^2 t) / r  =>  Gamma(sigma W - beta t) / h,    sigma^2 = E B^2 / E B,   h = E B^2 / (2 E B),

where Gamma is reflection at zero. Zwart asked this as Problem 1 of *Conjectures on symmetric queues in heavy traffic* (Queueing Systems 100 (2022), 369-371). It was known for processor sharing and for last-come-first-served. The proof is a uniform state-space collapse between the workload and h times the queue length. It uses the product-form stationary law with the original service requirements kept as marks, the regeneration at empty times, and a Bernstein bound over dyadic classes of original requirement.

## Contents

- `paper/main.tex`, `paper/main.pdf`: the paper.
- `code/checks.py`: simulates 288 paths under four disciplines (processor sharing, service to the middle position, service to the first or last position by the parity of n, half the server to each end) for deterministic and Pareto(3) service at r = 16, 32, 64, and checks the interpolation inequality of Section 2 at every event. Output in `code/checks_out.txt` and `code/numerical_checks.json`.
- `code/check_regeneration.py`: tests the cycle identity E Y = r p pi(S) for deterministic service against the exact value from the product form, 8,000 cycles per discipline. Output in `code/check_regeneration_out.txt` and `code/regeneration_checks.json`.
- `code/check_marked_cycles.py`: the same identity for a two-point service law with a predicate on the residual work of the large jobs. Output in `code/check_marked_cycles_out.txt` and `code/marked_cycle_checks.json`.
- `lean/GridBridge.lean`: the scalar step behind the interpolation inequality, checked with Lean 4 and Mathlib.

## Running

    cd code
    python checks.py > checks_out.txt
    python check_regeneration.py > check_regeneration_out.txt
    python check_marked_cycles.py > check_marked_cycles_out.txt

The scripts use only the Python standard library. The Lean file compiles inside any Lean 4 project with Mathlib (`lake env lean GridBridge.lean`).

## License

Paper: CC BY 4.0. Code: MIT.
