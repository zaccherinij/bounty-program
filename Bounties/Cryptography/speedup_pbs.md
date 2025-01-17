# Improve the programmable bootstrapping in TFHE
`Cryptography` `TFHE`

## Overview
Improve the efficiency of programmable bootstrapping in TFHE, for LWE inputs encrypting 4-bit integers, at least of a 10x factor, on a given machine. 

## Description
Implement a new variant of programmable bootstrapping of TFHE in Concrete, that achieves at least a 10x factor improvement.
Programmable bootstrapping is an operation that is able to reduce the noise inside a ciphertext and, at the same time, to evaluate a look-up table on the encrypted message.

#### Security and noise
 * The security level of the solution has to be at least 128 bits, strictly under the GLWE problem;
 * The error probability for the chosen parameter set should be at worse $2^{-40}$
 * The noise of the output ciphertext has to be such that at least 3 bits between the message and the noise are empty.

#### Performances and comparison with the state of the art
 * The new programmable bootstrapping must be able to bootstrap correctly a polynomial message with 4-bit coefficients, encrypted as one GLWE ciphertext, and provide in output a GLWE ciphertext encrypted under the same secret key;
 * The public key material (bootstrapping keys, key switching keys, ...) has to remain below 1GB in total;
 * The speed up must be proven by experimental results on the same architecture, **single-threaded**.

Your solution should compare to the following implementation from [TFHE-rs](https://github.com/zama-ai/tfhe-rs):
```
AWS m6i.metal (Intel(R) Xeon(R) Platinum 8375C CPU @ 2.90GHz)
OS: Ubuntu 22.04
```
The parameters for a single bootstrapping on this architechture are:
```
lwe_dimension: LweDimension(742),
glwe_dimension: GlweDimension(1),
polynomial_size: PolynomialSize(2048),
lwe_modular_std_dev: StandardDev(0.000007069849454709433),
glwe_modular_std_dev: StandardDev(0.00000000000000029403601535432533),
pbs_base_log: DecompositionBaseLog(23),
pbs_level: DecompositionLevelCount(1),
ks_level: DecompositionLevelCount(5),
ks_base_log: DecompositionBaseLog(3),
message_modulus: MessageModulus(4),
```

We use 64-bit integers in the implementation.
The key sizes and timings for a single bootstrapping on this architecture are:
```
Bootstrapping key: 46.38 MB
Bootstrapping key (Fourier): 92.75 MB
Key swiching key: 58.05 MB
Time per PBS single-thread (no avx512): 21.419 ms
Time per PBS single-thread (avx512): 18.396 ms
```

Your timings should be for a single pbs on a single thread, non-amortized.

#### Validity of the solutions proposed 
A valid submission contains the following:
 * A PDF format (using LaTeX) document, describing in detail the solution proposed;
 * An implementation using TFHE-rs, and instructions to run it; 
 * A set of tests aiming to prove the claim on efficiency and instructions to run them.

## Library targeted
[TFHE-rs](https://github.com/zama-ai/tfhe-rs)

## Bounty type 
Expert

## Reward
Rewards depends on the speedup achieved:
- 10-20x: €10,000
- 21-50x: €50,000
- 51-99x: €100,000
- 100x+:  €200,000

## Related links and references
The sources we provide are just indicative (not necessarily the most up to date results and not an exhaustive list of sources):
- TFHE paper: [CGGI20](https://eprint.iacr.org/2018/421);
- [TFHE deep dive](https://www.zama.ai/post/tfhe-deep-dive-part-1)
- [TFHE-rs](https://github.com/zama-ai/tfhe-rs)

## Submission
Apply directly to this bounty by sending an application [here](https://zama.ai/bounty-program-application).

## Questions?
Do you have a specific question about this bounty? Join the live conversation on the FHE.org discord server [here](https://discord.fhe.org). You can also send us an email at: bounty@zama.ai
