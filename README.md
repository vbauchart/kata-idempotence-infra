# kata idempotence infra

## Problem Statement

> Purpose: get a concrete grasp of what is idempotence for infrastructures, and why it's so important for modern systems

## Part 1 - Theory in practice with bash

*Let's dive gently into the topic of idempotence, in your bash terminal*

### Prerequisites:

- Install Bash or similar (you can use Cygwin Bash provided with GIT)
- Install BATS from https://github.com/bats-core/bats-core/

### Steps

*Please don't read further than one step at a time, to not get spoiled*

Run manually in a console:

```sh
// Run in console
> mkdir myApplication
> ls
> myApplication
```
It works because the folder didn't exist, obviously. But what if we run it again?

```sh
// Run again
> mkdir myApplication
> mkdir: myApplication: File exists
```

So what could you do? Discuss and propose options. Then we can consider them one at a time.


### Option 1

```sh
// Option 1: Ignore error
> mkdir -p myApplication
```

Run it multiple times. Problem solved. But is it really? What could go wrong now with this approach?

### Option 2

```sh
// Option 2: drop & recreate
> rm -rf myApplication && mkdir myApplication
```

Run it multiple times. Problem solved. That's how containers work. Discuss the pros and cons.

### Option 3

```sh
// Option 3: check & create
> test -d myApplication || mkdir myApplication
```

Run it multiple times. Problem solved. That's the idempotence you often want in practice.

Ok. So far we had to run again and check manually with `ls` that the folder was as we expected. How to test automatically without `ls` each time?

One way is to use a unit test framework like `bats`. Or simply using bash scripts.



### Test-driven scripts

Package the script into its own file `test_idempotent_script`) and execute it as a unit test with Bats:

```sh
bats tests/test_idempotent_script
```

Start by commenting out the mkdir line, to check the unit test fails, and then we uncomment to make it pass. Youpiii! That's how we can do Test-Driven in script! 

Now if you want your unit tests not to pollute your system, it's good practice to add `teardown()` and `setup()`, and a `canary test`, as in the example test file [here](https://github.com/vbauchart/kata-idempotence-infra/blob/main/tests/test_idempotent_script).


### Getting deeper into practical idempotence

Folder
- chmod
- chown
- append file
- append line into file

(TODO)

> Conclusion: A bundle of idempotent scripts is idempotent! Good news! If every little snippet is well done and idempotent, then any combination of them is already idempotent as well. Cool!

Imagine taking of all that manually, for 10 deploys a day, on 20 different machines. Discuss how idempotence could help reduce the operational burden.

Discuss how all this relates to Terraform infrastructure provisioning.


## Part 2 - Hands-on with Ansible, Puppet
