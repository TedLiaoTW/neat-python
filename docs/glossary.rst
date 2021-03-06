Glossary
=========

.. default-role:: any

.. glossary::
  :sorted:

  attributes
    These are the properties of a :term:`node` (such as its :term:`activation function`) or :term:`connection` (such as whether it is :term:`enabled` or not)
    determined by its associated :term:`gene` (in the default implementation, in the :py:mod:`attributes` module in combination with the gene class).

  activation function
  aggregation function
  bias
  response
    These are the :term:`attributes` of a :term:`node`. They determine the output of a node as follows:
    :math:`\begin{equation}\operatorname{activation}(bias + (response * \operatorname{aggregation}(inputs)))\end{equation}`
    For available activation functions, see :ref:`activation-functions-label`; for adding new ones, see :ref:`customization-label`.

  node
    Also known as a neuron (as in a *neural* network). They are of three types:
    :term:`input <input node>`, :term:`hidden <hidden node>`, and :term:`output <output node>`. Nodes have one or more :term:`attributes`, such
    as an :term:`activation function`; all are determined by their :term:`gene`. Classes of node genes include :py:class:`genes.DefaultNodeGene` and
    :py:class:`iznn.IZNodeGene`.

  input node
    These are the :term:`nodes <node>` through which the network receives inputs. They cannot be deleted (although :term:`connections <connection>`
    from them can be), cannot be the output end of a :term:`connection`, and have: no :term:`aggregation function`; a fixed :term:`bias` of 0; a
    fixed :term:`response` multiplier of 1; and a fixed :term:`activation function` of :ref:`identity <identity-label>`. Note: In the :py:mod:`genome` module,
    they are not in many respects treated as actual nodes, but simply as :term:`keys <key>` for input ends of connections. Sometimes known as an
    input :term:`pin`.

  hidden node
    These are the :term:`nodes <node>` other than :term:`input nodes <input node>` and :term:`output nodes <output node>`. In the original
    NEAT (NeuroEvolution of Augmenting Topologies) :doc:`algorithm <neat_overview>`, networks start with no hidden nodes, and evolve
    more complexity as necessary - thus "Augmenting Topologies".

  homologous
    Descended from a common ancestor; two genes in NEAT from different genomes are either homologous or :term:`disjoint`/excess. In NEAT, two
    genes that are homologous will have the same :term:`key`/id. For :term:`node` genes, the key is an `int` incremented with each newly-created node;
    for :term:`connection` genes, the key is a `tuple` of the keys of the nodes being connected. For further discussion, see the :ref:`neat-overview-label`.

  disjoint
  excess
    These are genes in NEAT not descended from a common ancestor - i.e., not :term:`homologous`. This implementation of NEAT, like most, does
    not distinguish between disjoint and excess genes. For further discussion, see the :ref:`neat-overview-label`.

  output node
    These are the :term:`nodes <node>` to which the network delivers outputs. They cannot be deleted (although :term:`connections <connection>` to
    them can be) but can otherwise be :term:`mutated <mutation>` normally. The output of this node is connected to the corresponding output :term:`pin`
    with an implicit :term:`weight`-1, :term:`enabled` connection.

  pin
    Point at which the network is effectively connected to the external world. Pins are either input (aka :term:`input nodes <input node>`) or output
    (connected to an :term:`output node` with the same :term:`key` as the output pin).

  weight
  enabled
    These are the :term:`attributes` of a :term:`connection`. If a connection is enabled, then the input to it (from a :term:`node`) is
    multiplied by the weight then sent to the output (to a node - possibly the same node, for a :term:`recurrent` neural network).
    If a connection is not enabled, then the output is 0; genes for such connections are the equivalent of `pseudogenes
    <http://pseudogene.org/background.php>`_ that, as in `in vivo <https://en.wikipedia.org/wiki/In_vivo>`_ evolution, can be reactivated at a later time.
    TODO: Some versions of NEAT give a chance, such as 25%, that a disabled connection will be enabled during :term:`crossover`; in the future, this
    should be an option.

  connection
    These connect between :term:`nodes <node>`, and give rise to the *network* in the term ``neural network``. For non-loopback (directly :term:`recurrent`)
    connections, they are equivalent to biological synapses. Connections have two :term:`attributes`, their :term:`weight` and whether or not they are
    :term:`enabled`; both are determined by their :term:`gene`. An example gene class for connections can be seen
    in :py:class:`genes.DefaultConnectionGene`.

  feedforward
  feed-forward
    A neural network that is not :term:`recurrent` is feedforward - it has no loops. (Note that this means that it has no memory - no ability to take into account
    past events.) It can thus be described as a `DAG (Directed Acyclic Graph) <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_.

  recurrent
    A recurrent neural network has cycles in its topography. These may be a :term:`node` having a :term:`connection` back to itself, with (for a
    :term:`discrete-time` neural network) the prior time period's output being provided to the node as one of its inputs. They may also have longer cycles,
    such as with output from node A going into node B (via a connection) and an output from node B going (via another connection) into node A. (This
    gives it a possibly-useful memory - an ability to take into account past events - unlike a :term:`feedforward` neural network; however, it also makes it
    harder to work with in some respects.)

  continuous-time
  discrete-time
    A discrete-time neural network (which should be assumed unless specified otherwise) proceeds in time steps, with processing at one :term:`node`
    followed by going through :term:`connections <connection>` to other nodes followed by processing at those other nodes, eventually giving the output.
    A continuous-time neural network, such as the :doc:`ctrnn <ctrnn>` (continuous-time :term:`recurrent` neural network) implemented in NEAT-Python,
    simulates a continuous process via differential equations (or other methods).

  genome
    The set of :term:`genes <gene>` that together code for a (neural network) phenotype. Example genome objects can be seen in
    :py:class:`genome.DefaultGenome` and :py:class:`iznn.IZGenome`, and the object interface is described in :ref:`genome-interface-label`.

  genomic distance
    An approximate measure of the difference between :term:`genomes <genome>`, used in dividing the population into :term:`species`. For further
    discussion, see the :ref:`neat-overview-label`.

  genetic distance
    The distance between two :term:`homologous` :term:`genes <gene>`, added up as part of the :term:`genomic distance`. Also sometimes used as
    a synonym for :term:`genomic distance`.

  gene
    The information coding (in the current implementation) for a particular aspect (:term:`node` or :term:`connection`) of a neural network phenotype.
    Contains several :term:`attributes`, varying depending on the type of gene. Example gene classes include :py:class:`genes.DefaultNodeGene`,
    :py:class:`genes.DefaultConnectionGene`, and :py:class:`iznn.IZNodeGene`; all of these are subclasses of :py:class:`genes.BaseGene`.

  species
    Subdivisions of the population into groups of similar (by the :term:`genomic distance` measure) individuals (:term:`genomes <genome>`),
    which compete among themselves but share fitness relative to the rest of the population. This is, among other things, a mechanism to try to avoid the
    quick elimination of high-potential topological mutants that have an initial poor fitness prior to smaller "tuning" changes. For further discussion,
    see the :ref:`neat-overview-label`.

  crossover
    The process in sexual reproduction in which two :term:`genomes <genome>` are combined. This involves the combination of :term:`homologous`
    genes and the copying (from the highest-fitness genome) of :term:`disjoint/excess <disjoint>` genes. Along with :term:`mutation`, one of the
    two sources of innovation in (classical) evolution.

  mutate
  mutation
    The process in which the :term:`attributes` of a :term:`gene` (or the genes in a :term:`genome`) are (randomly, with likelihoods determined by
    configuration parameters) altered. Along with :term:`crossover`, one of the two sources of innovation in (classical) evolution.

  id
  key
    Various of the objects used by the library are indexed by an key (id); for most, this is an `int`, which is either unique in the library as a whole
    (as with :term:`species` and :term:`genomes <genome>`), or within a genome (as with :term:`node` :term:`genes <gene>`).
    For :term:`connection` genes, this is a `tuple` of two `ints <int>`, the keys of the connected nodes.

:ref:`Table of Contents <toc-label>`
