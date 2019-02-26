Test gravity in simulation code of Farnes (2018)
Makes use of NumPy, DASK and probably other modules

This is the same code originally published by Dr J. Farnes in his
github repository, with some minor modifications to calculate and
print out the gravitational accleration imprinted on four test
particles by a central large mass. Details on the modifications are
below

******* How to run **********

1)Import relevant modules with something like:
import sys
sys.append(['./','negmass_nbody/','negmass_nbody/initialise/'])

2)Run pipe.py
You should get the following output:

In [4]: %run pipe
Initialising Dark matter halo formation simulation...
Saving initial conditions to disk...
Beginning N-body simulation. Iteration: 0 of 1000
distance=1.0, grav=-998.1666870117188
distance=2.0, grav=-499.5
distance=3.0, grav=-333.8333435058594
distance=4.0, grav=-251.8333282470703

******* Explanation **********

The original source code was obtained from Dr Farnes' repository at
https://github.com/jamiefarnes/negative-mass-simulator
Three small blocks of code were added to the source code. They are
marked with the comment # HSN

Block 1. File negmass_nbody/initialise/init.py, line 39
    # HSN
    epsilon = 0.
    num_pos_particles = 5
    num_neg_particles = 0
    chunks_value = (num_pos_particles+num_neg_particles)/5.0
    # 

Block 2. File negmass_nbody/initialise/init.py, line 166
    # HSN
    position=np.zeros((5,3))
    position[:,0]=[0.,1.,2.,3.,4.]
    velocity=np.zeros((5,3))
    mass=np.array([1000,1.,1.,1.,1.])
    #

Block 3. File negmass_nbody/simulate/sim.py, line 100

    # HSN
    for i in range(1,len(dx)):
        print ('distance={}, grav={}'.format(position.compute()[i,0], total_ax.compute()[i]))
    import sys
    sys.exit(0)


Explanation: Blocks 1 and 2 set up the initial conditions. They are
included as a hack to the "halo" simulation. Block 1 specifies the
simulation parameters, with only 5 particles (one large mass and four
test particles). No smoothing will be necessary so epsilon is set to 0
to avoid confusion. The gravitational constant had been set to 1 by
the original initialization. 

Block 2 establishes the particles initial positions and (zero)
velocities. The first particles has mass 1000 and is located at the
center of coordinates. The four test masses (mass unity) are placed at
a distance of 1, 2, 3 and 4, respectively.

Block 3 will simply print out the acceleration computed for each one
of the test particles. Since G=1, and neglecting the effect of the
mass particles on each other, the correct acceleration should be
100/d^2 (where d is the distance). However, when this test is run, we
obtain 100/d

distance=1.0, grav=-998.1666870117188
distance=2.0, grav=-499.5
distance=3.0, grav=-333.8333435058594
distance=4.0, grav=-251.8333282470703
