# Nodes Stacking and Graph Parsing for Deep Learning

Copyright (c) 2017, Yida Wang All rights reserved.

Use of this source code is governed by a BSD-style license that can be found in the LICENSE file.

## Important Components

### Nodes

Base class for nodes in the network.

Arguments:

`inbound_nodes`: A list of nodes with edges into this node.

```python
class Node:
```

Initiation for Class Nodes. Node's constructor (runs when the object is instantiated).

```python
    def __init__(self, inbound_nodes=[]):
        # A list of nodes with edges into this node.
        self.inbound_nodes = inbound_nodes
        # The eventual value of this node. Set by running
        # the forward() method.
        self.value = None
        # A list of nodes that this node outputs to.
        self.outbound_nodes = []
        # New property! Keys are the inputs to this node and
        # their values are the partials of this node with
        # respect to that input.
        self.gradients = {}
        # Sets this node as an outbound node for all of
        # this node's inputs.
        for node in inbound_nodes:
            node.outbound_nodes.append(self)
```

Every node that uses this class as a base class will need to define its own `forward` method.

```python
    def forward(self):
```

Every node that uses this class as a base class will need to define its own `backward` method.

```python
    def backward(self):
```

### Graph Parsing

Sort the nodes in topological order using Kahn's Algorithm.

`feed_dict`: A dictionary where the key is a `Input` Node and the value is the respective value feed to that Node. This method returns a list of sorted nodes.

```python
def topological_sort(feed_dict):
```

### Solver

Updates the value of each trainable with SGD.

Arguments:

`trainables`: A list of `Input` Nodes representing weights/biases. `learning_rate`: The learning rate.

```python
def sgd_update(trainables, learning_rate=1e-2):
```
