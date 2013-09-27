<a href="http://promises-aplus.github.com/promises-spec">
    <img src="http://promises-aplus.github.com/promises-spec/assets/logo-small.png"
         align="right" alt="Promises/A+ logo" />
</a>

# Promises/A+ Compliance Test Suite

This suite tests compliance of a promise implementation with the [Promises/A+ specification][].

[Promises/A+ specification]: https://github.com/promises-aplus/promises-spec

## How To Run

spin up a server, visit something in the tests directory, feel free to submit a pull with your library.

### Adapters

You need to have a global object called 'adapter' which the following keys:

- `fulfilled(value)`: creates a promise that is already fulfilled with `value`.
- `rejected(reason)`: creates a promise that is already rejected with `reason`.
- `pending()`: creates an object consisting of `{ promise, fulfill, reject }`:
  - `promise` is a promise that is currently in the pending state.
  - `fulfill(value)` moves the promise from the pending state to a fulfilled state, with fulfillment value `value`.
  - `reject(reason)` moves the promise from the pending state to the rejected state, with rejection reason `reason`.

The `fulfilled` and `rejected` exports are actually optional, and will be automatically created by the test runner using
`pending` if they are not present. But, if your promise library has the capability to create already-fulfilled or
already-rejected promises, then you should include these exports, so that the test runner can provide you with better
code coverage and uncover any bugs in those methods.

Note that the tests will never pass a promise or a thenable as a fulfillment value. This allows promise implementations
that only have "resolve" functionality, and don't allow direct fulfillment, to implement the `pending().fulfill` and
`fulfilled`, since fulfill and resolve are equivalent when not given a thenable.

Finally, note that none of these functions, including `pending().fulfill` and `pending().reject`, should throw
exceptions. The tests are not structured to deal with that, and if your implementation has the potential to throw
exceptions—e.g., perhaps it throws when trying to resolve an already-resolved promise—you should wrap direct calls to
your implementation in `try`/`catch` when writing the adapter.

### Examples

- [Lie](http://calvinmetcalf.github.io/promises-tests/examples/lie.html)
- [Q](http://calvinmetcalf.github.io/promises-tests/examples/q.html)
- [RSVP](http://calvinmetcalf.github.io/promises-tests/examples/rsvp.html)
- [When](http://calvinmetcalf.github.io/promises-tests/examples/when.html)

