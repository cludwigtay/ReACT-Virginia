# ReACT-Virginia
**Re**current **A**lgorithm **C**omputing **T**ransformer
Make Constructive Example -> Compute SAT computer algo -> Use as routing system.

# V1 Draft
## AC Construction Parameters
Transformer attends to various parts to construct parameters needed to build an algorithm.
This involves making short input examples that test edge cases.
Makes a set of training examples in increasing length. Assigns each training example an estimated compute length

## Computing Architecture
System to compute integers in order to direct mem addressing.
The goal is to make a generalized recurrent unit that, given memory tape, is turing complete.
Recurrent unit allows for easy generalizability. Repeated identical units to forward pass.
Each step take mem tape, apply repeated fixed seq of ops to make new tape, repeat.
### OPs
OP1 take 2 items from either memory or static and writes to cache or memory

Memory addressing based on cache

OPS: +,*,//,MAX,MIN

### Memory
Main input tape, initialized with input only, index -1 is input length.
Output is taken from the same first n cells of the tape
Each cell can have an int.
Alongside input tape is cache fixed len mem.
Static for unwritable numbers.
Cache has 2 input 1, and 2 input 2 slots.

# V2 Draft
## AC Construction parameters 
Transformer makes examples with apriory of how to solve. Still constructs computing system through examples. Examples include input in string to output strings. Information routing graphs, sequence of binary ops, learn program that takes ints and makes an addressing program that can calculate integer pos correctly over many examples with recurrence. Computing systems should be highly parallel (Transformer like) to leverage simplicity of many common tasks.


# Optimizer
Relate backprop to differentiable SATMax


# Computation

110 mil param model: 155.112 min for 1xA100. 0.01873358730628398 $/A100 min. 3$ @ 2.6 hrs for BERT

1 Bil param will yield acceptable results, ~80% nlp. 1410.11 min, 26.416$ @ 23.5 hrs
