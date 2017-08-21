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

## Spys, Stubs and Mocks

### Spys
It gives us a fake function that we can use track execution;

Also allows us to watch a different function;

```javascript
```

### Stubs
It takes an object/function and replace it with something else. That allows us to controll its behavior, return what we're expecting, throw exceptions, etc.

```javascript
```

### Mocks
Combined behaviors from `Spys` and `Stubs`. Plus pre-programmed expectations.

We first define how we want things to work then we verify it at the end.

```javascript
```