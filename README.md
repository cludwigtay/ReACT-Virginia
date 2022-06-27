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
Transformer makes examples with apriory of how to solve. Still constructs computing system through examples. Examples include input in string to output strings. Information routing graphs, sequence of binary ops, learn program that takes ints and makes an addressing program that can calculate integer pos correctly over many examples with recurrence. ~~Computing systems should be highly parallel (Transformer like) to leverage simplicity of many common tasks~~.

Routing notation: Routing takes binary op: & a pair or indices and writes to a write ind. Perform sequentially

### Example: Bitwise addition
0123456
1001+11
1100---

Routing:
**3 & 6 = 3**

3 & 2 = 2
2 & 5 = 2

2 & 1 = 1
1 & 

1 & 0 = 0


The goal is to figure out routing rules using a few simple examples.

Preprocessing stage: Figure out rules to make initial numbers: 3, 6
Remaining numbers can be calculated using a set of static numbers : 3, 6, 1, -1, 0

Make an algorithm with access to the input seq and static numbers, resulting in a list of binary ops.
At each step, the algorithm has a pair of int pointers and has access to static numbers and the numbers pulled by indexes in current and temp tape
The 2 pointers can write to a temp tape at the spots

Options at each step: take both as string, pass, write to mem.

# V3 Draft
Many components to merge the benefits of multiple model types.

ReACT:

input -> Conduit  -c-             input -> Conduit  -c-
                  + -> SATrans -> 
input -> ARes     -d-             input -> ARes     -d-

Shared weights, recurrent unit.
Decoder blocks are standard decoder attention units

## UNIT Block 3
  Universal transformer block.
                                        3 Conv
  input -> Norm -> Gated linear unit -> Norm -> 11 sep conv -> relu            -> Norm -> 11 sep conv -> self attention -> Norm -> Lin -> Relu -> lin
                                        Counting Transformer -> relu 
        -----------------------------+ -----------------------------------------+              -------------------------+ -------------------------+
## Conduit 4
  c runs continuously through network
  input -> UNIT1 -> LSTM1 I -> LSTM1 O -> lin -> UNIT2 -> LSTM2 I -> LSTM2 O -> lin
             -------------------------------+          -----------------------------+
  recursive unit

## AResBenes 2
  Benes block with ARes switch unit

### ARes switch 1
  (d1|d2|c -> iNalu -> B+ B0 B- gates) | s1 | s2 -> lin lin -> temp -> s'1|s'2
   temp -> lin -> Wa, Ma, Wm, Mm
   d1|d2|c -> iCNALU(Wa,Ma,Wm,Mm) -> d1|d2
   
## SATrans 5
  d expressions, 2d head transformer. tanh() x sigmoid()
  seq|buffer -> Norm -> downscale lin -> Norm -> self attend -> solve -> bin vec
  
  output = line(bin vec) + seq
  
  
## Neural Adjacency Network
- Neural Networks traditionally transfer information through vectors
- Attention is sort of adj mat like.
- Transmit information in adj mat
- One problem with adj mat info transfer is permutations of input.
- System has to be able to do regular info graph transmission
- System has to easily expand graph in large chunks.
- System has to easily compress graph through subgraph selection.
  


# Optimizer
Relate backprop to differentiable SATMax


# Computation

110 mil param model: 155.112 min for 1xA100. 0.01873358730628398 $/A100 min. 3$ @ 2.6 hrs for BERT

1 Bil param will yield acceptable results, ~80% nlp. 1410.11 min, 26.416$ @ 23.5 hrs
