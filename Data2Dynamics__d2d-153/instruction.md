# Issue

**Title:** Minor change: conversion to symbolic in MATLAB2020a

## Description

It seems MATLAB2020a cannot convert some char strings to symbolic arrays. Apparently, the problem is because the expression which is going to be converted is a column vector. By replacing it with a row vector, MATLAB can handle the conversion. What I suggest is explicitly replacing semicolons with commas in MATLAB2020a and later versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `721f46f6997c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.