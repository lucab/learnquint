# Actions

## Overview

Actions are defined through the keyword `action`.
An action is a user-defined operator which specifies how a model can evolve over time.

Each specification must define at least two actions:
 1. an initialization entry (usually named `init`) which is executed exactly once as the entrypoint of the model.
 2. a stepping entry (usually named `step`) which is executed in a infinite loop, and drives forward the model evolution over time.

## Example

The example below is called `actions.qnt` and contains a valid model that does nothing, forever. 

```
{{#include ../specs/actions.qnt}}
```

## Further notes

Actions are typed, but type-signatures are optional and can be automatically inferred.
That is, `action init: bool` and `action init` are equivalent syntax.

Both `init` and `step` actions return a `bool`, which has the following meaning:
 - `true`: the action can be selected and executed by the model checker (i.e. it is "enabled").
 - `false`: the action cannot be selected and executed by the model checker (i.e. it is not "enabled").

Changing one (or both) of the actions in example above to `false` results in a deadlock: the model checker will reach a state where it cannot progress further, as it has no valid action to select anymore.
