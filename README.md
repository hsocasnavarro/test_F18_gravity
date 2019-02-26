# test_F18_gravity
Test gravity in simulation code of Farnes (2018)  
  
  
Check details in the included README.txt  

  
  
Makes use of NumPy, DASK and probably other modules

1)Import relevant modules with something like:  
import sys  
sys.append(['./','negmass_nbody/','negmass_nbody/initialise/'])

2)Run pipe.py  
  You should get the following output:  
    
In [4]: %run pipe  
Initialising Dark matter halo formation simulation...  
Saving initial conditions to disk...  
Beginning N-body simulation. Iteration: 0 of 1000  
distance=1.0, grav=-999.9982299804688  
distance=2.0, grav=-499.99951171875  
distance=3.0, grav=-333.3338317871094  
distance=4.0, grav=-250.00184631347656  
