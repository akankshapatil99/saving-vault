# SCS Lab 4: Savings Vault Security Audit

This repository contains a compact smart-contract security lab focused on identifying vulnerabilities in a savings vault, fixing the root issues, and validating the remediation with tests and static analysis.

## Overview

The project includes two contracts:

- `contracts/SavingsVault.sol` — the vulnerable baseline implementation used for audit and comparison.
- `contracts/SavingsVaultFixed.sol` — the hardened version with the security fixes applied.

The workflow follows a realistic audit cycle:

1. Review the original contract for security weaknesses.
2. Run automated tests and static analysis.
3. Document the findings and recommended fixes.
4. Implement the revised contract.
5. Verify the remediation with regression checks.

## Project Structure

```text
SCS-lab_Unit4/
├── contracts/
│   ├── SavingsVault.sol
│   └── SavingsVaultFixed.sol
├── test/
│   ├── SavingsVault.t.sol
│   ├── SavingsVaultFixed.t.sol
│   └── SavingsVault.ts
├── scripts/
│   └── send-op-tx.ts
├── AGENTS.md
├── CLAUDE.md
├── README.md
├── audit-findings.md
├── audit-summary.md
├── hardhat.config.ts
├── manual-checklist.md
├── package.json
├── package-lock.json
├── slither-report.txt
├── slither-fixed-report.txt
├── tsconfig.json
└── .gitignore
```

## Security Findings Covered

The original vault was reviewed for the following common issues:

- Reentrancy in the withdrawal flow
- Abuse of `tx.origin` for authorization
- Lack of zero-address validation
- Unbounded fee configuration
- Missing event emission for fee-related actions
- Unsafe transfer behavior and insufficient validation
- Non-immutable owner state

The fixed contract addresses these concerns with stricter checks, event logging, access control, and reentrancy protection.

## Audit Documentation

- `audit-summary.md` — high-level summary of the findings and the remediation plan.
- `audit-findings.md` — issue-by-issue impact and fix details.
- `manual-checklist.md` — manual audit checklist used during review.
- `slither-report.txt` — static analysis output for the original contract.
- `slither-fixed-report.txt` — static analysis output for the fixed contract.

## Tech Stack

- Solidity 0.8.x
- Hardhat
- TypeScript test tooling
- OpenZeppelin Contracts
- Slither
- Node.js and npm

## Quick Start

Install dependencies:

```bash
npm install
```

Run the test suite:

```bash
npx hardhat test
```

Run Slither against the original vault:

```bash
slither contracts/SavingsVault.sol
```

Run Slither against the fixed vault:

```bash
slither contracts/SavingsVaultFixed.sol --solc-remaps "@openzeppelin/=$(pwd)/node_modules/@openzeppelin/"
```

## Notes

This project is intended as a learning and audit exercise. It demonstrates how to identify smart-contract weaknesses, document them, and validate a hardened remediation. The security findings and fixes are educational, and the audit artifacts should be reviewed in context before any production deployment.
