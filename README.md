# kata idempotence infra

## Problem Statement

> Purpose: get a concrete grasp of what is idempotence for infrastructures, and why it's so important for modern systems

## Part 1 - Theory in practice with bash

Prerequisites:

- Install Bash or similar (you can use Cygwin Bash provided with GIT)
- Install BATS from https://github.com/bats-core/bats-core/

### Let's introduce idempotence gently on your console

Run manually in a console :

```sh
// Run

> mkdir myApplication

> ls

> myApplication

// Run again

> mkdir myApplication

> mkdir: myApplication: File exists

What could you do?

// Ignore error

> mkdir -p myApplication

// But what could go wrong?

// drop & recreate

> rm -rf myApplication && mkdir myApplication

// But what could go wrong?

// Run again multiple times & check with 'ls'

// How to test without ls each time?
```

Execute Bats testu :

```sh
bats tests/test_idempotent_script
```

## Part 2 - Hands-on with Ansible, Puppet
