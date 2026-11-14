# Practical 06: DFA to Regular Grammar Conversion

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krishna Lohana  
**Roll No:** 29  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Date of Submission:** 14 November 2026 (14-11-2026)  
**Source DFA File:** [`29_Krishna_Lohana_DFA_Source_14-11-2026.jff`](29_Krishna_Lohana_DFA_Source_14-11-2026.jff)  
**Converted Grammar File:** [`29_Krishna_Lohana_Grammar_Converted_14-11-2026.jff`](29_Krishna_Lohana_Grammar_Converted_14-11-2026.jff)

---

## 1. Aim
To systematically convert a Deterministic Finite Automaton (DFA) recognizing binary strings starting with `0` and ending with `1` into an equivalent **Right-Linear Regular Grammar** in JFLAP.

---

## 2. Problem Statement
Let $\Sigma = \{0, 1\}$. The language $L$ is defined as:
$$L = \{ w \in \{0, 1\}^* \mid w \text{ begins with } 0 \text{ and terminates with } 1 \} = 0(0+1)^*1$$

---

## 3. Algorithmic Transformation Rules
For each state $q_i \in Q$, introduce a non-terminal variable $V_i$:
- $q_0 \implies S$ (Start variable)
- $q_1 \implies A$ (Started with `0`, currently ends in `0`)
- $q_2 \implies B$ (Started with `0`, currently ends in `1` - Final state)
- $q_3$ is a trap/dead state that produces no terminal strings and is pruned.

**Transformation Rules:**
1. For every transition $\delta(q_i, a) = q_j$, create production $V_i \to a V_j$.
2. For every final state $q_k \in F$, add the terminating production $V_k \to \epsilon$.

**Resulting Right-Linear Grammar:**
- $S \to 0A$
- $A \to 0A \mid 1B$
- $B \to 0A \mid 1B \mid \epsilon$

---

## 4. Grammar Derivation Example
Derivation of string `0101` $\in L$:
$$S \implies 0A \implies 01B \implies 010A \implies 0101B \implies 0101\epsilon = 0101$$

---

## 5. Test Suite & Verification
| String | Pattern | DFA Outcome | Grammar Derivation | Status |
|:---:|:---:|:---:|:---:|:---:|
| `01` | Starts 0, Ends 1 | Accept | $S \to 0A \to 01B \to 01$ | **MATCH** |
| `001` | Starts 0, Ends 1 | Accept | $S \to 0A \to 00A \to 001B \to 001$ | **MATCH** |
| `0111` | Starts 0, Ends 1 | Accept | Verified | **MATCH** |
| `0101` | Starts 0, Ends 1 | Accept | Verified | **MATCH** |
| `101` | Starts 1 (Invalid) | Reject | No derivation from $S$ | **MATCH** |
| `000` | Ends 0 (Invalid) | Reject | Cannot terminate in $A$ | **MATCH** |
| `11` | Starts 1 (Invalid) | Reject | No derivation from $S$ | **MATCH** |
| `0` | Length 1 (Invalid) | Reject | Cannot terminate in $A$ | **MATCH** |
