---
layout: post
title: Notes regarding Rails 4 Test Prescriptions
---

Chapter 1 and 2: Introduction and TDD Basics

- Basic stuff. The essentials of TDD and using the specs to steer design. 

Chapter 3: Test-Driven Rails

- I like the idea of an Action class. The notion being that non-boilerplate controller code (used to construct the model instance upon the Create action, for example) should have it's opwn Action class (CreatesProject)

- Using specify as a replacement for it blocks that do not require a description. 

- Outide in TDD; writing an end-to-end feature test and then working on the unit tests under the appropriate veticals (model, controller, etc.) that bring it together. 

Chapter 4: Whats Makes Great Tests

- Tests should be SWIFT, or Straightfoward, Well defined, Independent, Fast, and Truthful. 

Chapter 5: Testing Models

- Testing order: initial state, simplest happy path, alternate happy paths, sad/error and edge paths

- For the problem of multiple expect statements in a spec, the solution is to flush out the pattern that replaces "expect" with "specify" first seen in Ch. 3. For multiple assertions "put each assertion in a separate test and put the common setup in a setup block... The tradeoff is pretty plain: the one-assertion-per-test style has the advantage that each assertion can fail independently—when all the assertions are in a single test, the test bails on the first failure." 

- On testing associations: "you shouldn’t start from the idea that your [first model] belongs to a [second model]. Rather, as you describe features the relationship is implied from the feature tests that you’re writing. More operationally, this means that in a good TDD process, any condition in the code that would cause a direct test like those Shoulda matchers to fail would also cause another test to fail."

- On testing validations: "typically test for the functional effect of an invalid object rather than the implementation fact of the existence of a Rails validation. The functional effect is often along the lines of an object or objects not saving to the database." => Test behavior, not implementation. 

- You can write your own RSpec matchers via `RSpec::Matchers.define`.

Chapter 6: Managing Test Data