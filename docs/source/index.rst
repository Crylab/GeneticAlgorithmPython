.. PyGAD documentation master file, created by
   sphinx-quickstart on Sat May 16 15:14:25 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.





PyGAD - Python Genetic Algorithm!
=================================

`PyGAD <https://github.com/ahmedfgad/GeneticAlgorithmPython>`__ is an
open-source Python library for building the genetic algorithm and
optimizing machine learning algorithms. It works with
`Keras <https://keras.io>`__ and `PyTorch <https://pytorch.org>`__.

   Try the `Optimization Gadget <https://optimgadget.com>`__, a free
   cloud-based tool powered by PyGAD. It simplifies optimization by
   reducing or eliminating the need for coding while providing
   insightful visualizations.

`PyGAD <https://github.com/ahmedfgad/GeneticAlgorithmPython>`__ supports
different types of crossover, mutation, and parent selection operators.
`PyGAD <https://github.com/ahmedfgad/GeneticAlgorithmPython>`__ allows
different types of problems to be optimized using the genetic algorithm
by customizing the fitness function. It works with both single-objective
and multi-objective optimization problems.

.. image:: https://user-images.githubusercontent.com/16560492/101267295-c74c0180-375f-11eb-9ad0-f8e37bd796ce.png
   :alt: 

*Logo designed by* `Asmaa
Kabil <https://www.linkedin.com/in/asmaa-kabil-9901b7b6>`__

Besides building the genetic algorithm, it builds and optimizes machine
learning algorithms. Currently,
`PyGAD <https://pypi.org/project/pygad>`__ supports building and
training (using genetic algorithm) artificial neural networks for
classification problems.

The library is under active development and more features added
regularly. Please contact us if you want a feature to be supported.

.. _donation--support:

Donation & Support
==================

You can donate to PyGAD via:

-  `Credit/Debit Card <https://donate.stripe.com/eVa5kO866elKgM0144>`__:
   https://donate.stripe.com/eVa5kO866elKgM0144

-  `Open Collective <https://opencollective.com/pygad>`__:
   `opencollective.com/pygad <https://opencollective.com/pygad>`__

-  PayPal: Use either this link:
   `paypal.me/ahmedfgad <https://paypal.me/ahmedfgad>`__ or the e-mail
   address ahmed.f.gad@gmail.com

-  Interac e-Transfer: Use e-mail address ahmed.f.gad@gmail.com

-  Buy a product at `Teespring <https://pygad.creator-spring.com/>`__:
   `pygad.creator-spring.com <https://pygad.creator-spring.com>`__

Installation
============

To install `PyGAD <https://pypi.org/project/pygad>`__, simply use pip to
download and install the library from
`PyPI <https://pypi.org/project/pygad>`__ (Python Package Index). The
library lives a PyPI at this page https://pypi.org/project/pygad.

Install PyGAD with the following command:

.. code:: python

   pip3 install pygad

Quick Start
===========

To get started with `PyGAD <https://pypi.org/project/pygad>`__, simply
import it.

.. code:: python

   import pygad

Using `PyGAD <https://pypi.org/project/pygad>`__, a wide range of
problems can be optimized. A quick and simple problem to be optimized
using the `PyGAD <https://pypi.org/project/pygad>`__ is finding the best
set of weights that satisfy the following function:

.. code:: 

   y = f(w1:w6) = w1x1 + w2x2 + w3x3 + w4x4 + w5x5 + w6x6
   where (x1,x2,x3,x4,x5,x6)=(4,-2,3.5,5,-11,-4.7) and y=44

The first step is to prepare the inputs and the outputs of this
equation.

.. code:: python

   function_inputs = [4,-2,3.5,5,-11,-4.7]
   desired_output = 44

A very important step is to implement the fitness function that will be
used for calculating the fitness value for each solution. Here is one.

If the fitness function returns a number, then the problem is
single-objective. If a ``list``, ``tuple``, or ``numpy.ndarray`` is
returned, then it is a multi-objective problem (applicable even if a
single element exists).

.. code:: python

   def fitness_func(ga_instance, solution, solution_idx):
       output = numpy.sum(solution*function_inputs)
       fitness = 1.0 / numpy.abs(output - desired_output)
       return fitness

Next is to prepare the parameters of
`PyGAD <https://pypi.org/project/pygad>`__. Here is an example for a set
of parameters.

.. code:: python

   fitness_function = fitness_func

   num_generations = 50
   num_parents_mating = 4

   sol_per_pop = 8
   num_genes = len(function_inputs)

   init_range_low = -2
   init_range_high = 5

   parent_selection_type = "sss"
   keep_parents = 1

   crossover_type = "single_point"

   mutation_type = "random"
   mutation_percent_genes = 10

After the parameters are prepared, an instance of the **pygad.GA** class
is created.

.. code:: python

   ga_instance = pygad.GA(num_generations=num_generations,
                          num_parents_mating=num_parents_mating, 
                          fitness_func=fitness_function,
                          sol_per_pop=sol_per_pop, 
                          num_genes=num_genes,
                          init_range_low=init_range_low,
                          init_range_high=init_range_high,
                          parent_selection_type=parent_selection_type,
                          keep_parents=keep_parents,
                          crossover_type=crossover_type,
                          mutation_type=mutation_type,
                          mutation_percent_genes=mutation_percent_genes)

After creating the instance, the ``run()`` method is called to start the
optimization.

.. code:: python

   ga_instance.run()

After the ``run()`` method completes, information about the best
solution found by PyGAD can be accessed.

.. code:: python

   solution, solution_fitness, solution_idx = ga_instance.best_solution()
   print("Parameters of the best solution : {solution}".format(solution=solution))
   print("Fitness value of the best solution = {solution_fitness}".format(solution_fitness=solution_fitness))

   prediction = numpy.sum(numpy.array(function_inputs)*solution)
   print("Predicted output based on the best solution : {prediction}".format(prediction=prediction))

.. code:: 

   Parameters of the best solution : [3.92692328 -0.11554946 2.39873381 3.29579039 -0.74091476 1.05468517]
   Fitness value of the best solution = 157.37320042925006
   Predicted output based on the best solution : 44.00635432206546

There is more to do using PyGAD. Read its documentation to explore the
features of PyGAD.

PyGAD's Modules
===============

`PyGAD <https://pypi.org/project/pygad>`__ has the following modules:

1.  The main module has the same name as the library ``pygad`` which is
    the main interface to build the genetic algorithm.

2.  The ``nn`` module builds artificial neural networks.

3.  The ``gann`` module optimizes neural networks (for classification
    and regression) using the genetic algorithm.

4.  The ``cnn`` module builds convolutional neural networks.

5.  The ``gacnn`` module optimizes convolutional neural networks using
    the genetic algorithm.

6.  The ``kerasga`` module to train `Keras <https://keras.io>`__ models
    using the genetic algorithm.

7.  The ``torchga`` module to train `PyTorch <https://pytorch.org>`__
    models using the genetic algorithm.

8.  The ``visualize`` module to visualize the results.

9.  The ``utils`` module contains the operators (crossover, mutation,
    and parent selection) and the NSGA-II code.

10. The ``helper`` module has some helper functions.

The documentation discusses these modules.

PyGAD Citation - Bibtex Formatted
=================================

If you used PyGAD, please consider citing its paper with the following
details:

.. code:: 

   @article{gad2023pygad,
     title={Pygad: An intuitive genetic algorithm python library},
     author={Gad, Ahmed Fawzy},
     journal={Multimedia Tools and Applications},
     pages={1--14},
     year={2023},
     publisher={Springer}
   }


.. _header-n4:

pygad Module
===============


.. toctree::
   :maxdepth: 4
   :caption: pygad Module TOC

   pygad.rst



.. _header-n5:

More About pygad Module
===============


.. toctree::
   :maxdepth: 4
   :caption: More About pygad Module TOC

   pygad_more.rst




.. _header-n6:

utils Module
===============


.. toctree::
   :maxdepth: 4
   :caption: utils Module TOC

   utils.rst



.. _header-n7:

visualize Module
===============


.. toctree::
   :maxdepth: 4
   :caption: visualize Module TOC

   visualize.rst



.. _header-n8:

helper Module
===============


.. toctree::
   :maxdepth: 4
   :caption: helper Module TOC

   helper.rst




.. _header-n9:

pygad.nn Module
===============


.. toctree::
   :maxdepth: 4
   :caption: pygad.nn Module TOC

   nn.rst





.. _header-n10:

pygad.gann Module
=================


.. toctree::
   :maxdepth: 4
   :caption: pygad.gann Module TOC

   gann.rst









.. _header-n11:

pygad.cnn Module
=================


.. toctree::
   :maxdepth: 4
   :caption: pygad.cnn Module TOC

   cnn.rst



.. _header-n12:

pygad.gacnn Module
=================


.. toctree::
   :maxdepth: 4
   :caption: pygad.gacnn Module TOC

   gacnn.rst




.. _header-n13:

pygad.kerasga Module
=================


.. toctree::
   :maxdepth: 4
   :caption: pygad.kerasga Module TOC

   kerasga.rst




.. _header-n14:

pygad.torchga Module
=================


.. toctree::
   :maxdepth: 4
   :caption: pygad.torchga Module TOC

   torchga.rst


.. _header-n15:

Releases
=================


.. toctree::
   :maxdepth: 4
   :caption: Releases

   releases.rst




Indices and tables
==================

* :ref:`search`
