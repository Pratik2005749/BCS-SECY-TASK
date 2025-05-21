# BCS-SECY-TASK(DANCE OF PLANETS): PREICTING POSITIONS OF BODIES UNDER MUTUAL GRAVITATION AT ANY TIME USNG NEURAL NETWORKS

The main challenge in this task was to create your own training and testing dataset to train and test the model. The input parameters are masses of two bodies(m1 and m2),positions of the two bodies((x1,y1) and (x2,y2)), velocity vectors of the two bodies((v1x,v1y) and (v2x,v2y)), and time t at which we need to find the position. We had to predict final positions at time t((X1,Y1) and (X2,Y2)). All these parameters form the columns of the CSV files. Two methods were used to generate the dataset:

   # EULER INTEGRATION METHOD
   The main idea is to divide the time interval [0,t] in small time intervals and in those time intervals we assume forces,acclerations remain constant for calculation
   purpose and calculate new coordinates and then repeat this process till time t. If we use this method then we can use Newton's law of gravitation and equations of 
   motion to predict the coordinates. Finally using random() function we generate random input parametes within some predefined range and using Euler approach we 
   calculate the output parameters and create a csv file.

   # SOLVE_IVP METHOD USING RK45
   The accuracy of this method more than Euler approach but in this task we could not improve coordinate accuracy upto fourth decimal place. SOLVE_IVP is a method 
   which solves an initial value problem and stores all related information related to it. The method used to solve the differential equation was Runge-Kutta method
   of order 5(4) which is a numerical approach to approximate solutions of ODE.

   The training dataset has 100000 datapoints and testing dataset has 25000 datapoints.

The next step is to train a Neural Network and test its performance using MAE(Mean Absolute Error). I used three approaches to train aneural Network

  # USUAL NEURAL NETWORK
  I defined a primitive neural network architecture and trained it on the training dataset and tested it on testing dataset and got MAE of 0.65 which is not good 
  enough so need some improvement.

  To improve we will use a modifies Neural Network called PHYSICS INFORMED NEURAL NETWORK called PINN in short. PINN is different from NN because along with 
  focussing on dataset it considers the underlying physical law governing the motion which can increase model performance. The two approaches used were:

  # PARTIAL PINN
  I call this partial PINN because it considers how the input parameters change and tries to minimise the loss with respect to the parameters using physics loss.
  But it does not consider the physical law. The overall accuracy of this approach was 0.15

  # COMPLETE PINN
  In this method I consider the Newtons gravitation law as well. The main idea is to learn the dataset ensuring the model learns the underlying governing as well.
  The overall MAE was 0.35
