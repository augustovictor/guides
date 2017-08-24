# Nodejs Testing with Mocha

- Mocha as test runner;
- Chai for asserts;
- Sinon for mocking;

## Types of test

### Unit
Find the smallest piece and test just that and mock everything else;

### Integration
Testing the units together and interactions with `sinons` and `spy`.
Mock the outside resources. E.g., database or api;

### Functional
Black box testing.
It tests the entire application. End-to-end;

## Assertion with Chai

There are two ways of doing assertion with `chai`: `expect` and `should`. Both have the same effect;

## Test doubles
We can split types of functions into two categories:

**Functions without side effects** are simple: the result of such a function is only dependent on its parameters — the function always returns the same value given the same parameters.

**Function with side effects** can be defined as a function that depends on something external, such as the state of some object, the current time, a call to a database, or some other mechanism that holds some kind of state. The result of such a function can be affected by a variety of things in addition to its parameters.

## Spys, Stubs and Mocks

### Spys
It gives us a fake function that we can use track execution;

Also allows us to watch a different function;

Most common scenarios with **Spies**:

- Checking how many times a function was called
- Checking what arguments were passed to a function

### Stubs
It takes an object/function and replace it with something else. That allows us to controll its behavior, return what we're expecting, throw exceptions, etc.

Most common scenarios with **Stubs**:

- You can use them to replace problematic pieces of code
- You can use them to trigger code paths that wouldn't otherwise trigger - such as error handling
- You can use them to help test asynchronous code more easily

### Mocks
Combined behaviors from `Spys` and `Stubs`. Plus pre-programmed expectations.

We first define how we want things to work then we verify it at the end.

