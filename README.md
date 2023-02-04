# Hopfield-Network-Associative-Memory-Design
A Hopfield network is a type of spin glass system and a recurrent artificial neural network that was developed by John Hopfield in 1982 after being first described by Little in 1974 and based on Ernst Ising and Wilhelm Lenz's work on the Ising model. Hopfield networks function as content-addressable ("associative") memory systems for continuous variables or binary threshold nodes. Hopfield networks offer a model for comprehending human memory as well.
## Structure
The units in Hopfield nets are binary threshold units, i.e. the units only take on two different values for their states, and the value is determined by whether or not the unit's input exceeds its threshold U_i. Discrete Hopfield nets describe relationships between binary (firing or not-firing) neurons 1, 2, .., i, j, N . At a certain time, the state of the neural net is described by a vector V, which records which neurons are firing in a binary word of N bits. The interactions w_ij between neurons have units that usually take on values of 1 or −1. These interactions are "learned" via Hebb's law of association, such that, for a certain state V^s : </br>
![image](https://user-images.githubusercontent.com/78887209/216768306-01e30f55-f9b0-4e4e-b52a-811802f624ed.png) </br>
Once the network is trained, w_ij no longer evolve. If a new state of neurons V^s' is introduced to the neural network, the net acts on neurons such that :  </br>
![image](https://user-images.githubusercontent.com/78887209/216768375-67354ef7-6c73-45bf-9085-f719cf0b5163.png) </br>
where U_i is the threshold value of the i'th neuron (often taken to be 0). In this way, Hopfield networks have the ability to "remember" states stored in the interaction matrix, because if a new state V^s' is subjected to the interaction matrix, each neuron will change until it matches the original state V^s. The connections in a Hopfield net typically have the following restrictions: </br>
![image](https://user-images.githubusercontent.com/78887209/216768453-67cffb1a-48a0-4056-9690-8204ba1aaa5f.png) </br>
The constraint that weights are symmetric guarantees that the energy function decreases monotonically while following the activation rules. A network with asymmetric weights may exhibit some periodic or chaotic behaviour; however, Hopfield found that this behavior is confined to relatively small parts of the phase space and does not impair the network's ability to act as a content-addressable associative memory system. </br>
Hopfield also modeled neural nets for continuous values, in which the electric output of each neuron is not binary but some value between 0 and 1.[4] He found that this type of network was also able to store and reproduce memorized states. </br>
Notice that every pair of units i and j in a Hopfield network has a connection that is described by the connectivity weight  w_ij. In this sense, the Hopfield network can be formally described as a complete undirected graph G = <V,f> , where V is a set of McCulloch–Pitts neurons and f:V^2 --> R is a function that links pairs of units to a real value, the connectivity weight. Below is the structure of a four-unit hopfield network: </br>
![image](https://user-images.githubusercontent.com/78887209/216770875-5404c659-e0e3-4e44-b5b3-e8c4726c3f76.png)
## Application
For the Hopfield network design, 4 matrices of 5x10 size, consisting of 1s and -1s similar to 0,2,4,7 as digital numbers, were created.
![image](https://user-images.githubusercontent.com/78887209/216769123-a82a1d5b-2a99-4c17-bed6-3bbdbcad0580.png)
### Discrete Time Hopfield Network Associative Memory Design
#### 1.Creating the Memory
First of all, the weights had to be determined for the first stage, the Memory Creation stage. It was preferred to calculate the weights in advance and a weight matrix suitable for the data was created. The weight matrix suitable for the data and the Hopfield network must be symmetrical. In summary, the weight matrix was created by using the patterns that were created and wanted to be placed in the memory, and thus stable equilibrium point patterns were obtained. The Network is ready for the Recall phase.
#### 2.Recall
As a first condition, a total of 8 data were presented to the network, one noisy data from each data type and one random pixels made negative. Below you can see some data presented to the network as an initial condition. </br>
![image](https://user-images.githubusercontent.com/78887209/216769368-a84cdcd8-b034-4eb0-8207-69f2adc8ceb9.png) ![image](https://user-images.githubusercontent.com/78887209/216769375-a163a238-274a-49da-9b59-36b3d160a02d.png) </br>
The activation function is defined as 'if the current data is greater than 0, set the data equal to 1, if it is less than 0, equal the data to -1, if it is 0, equal the data of the x matrix in the previous step in that index'. Afterwards, we converted the corrupted data into a matrix (50.1) for ease of presentation to the network and combined them into a single numpy array containing 8 corrupted data. You can see the name of this numpy array in the codes as 'list_of_ilkkosul'. </br>
We took the first data (x(k)) and multiplied it with the weight matrix created during the memory creation phase, passing the result through the previously defined activation function, x(k+1) was obtained. The stopping criterion is that x(k+1) is equal to x(k). By adding this stopping criterion, the processes described above were applied to 8 corrupted records. </br>
The designed discrete-time associative hopfield network detects both kinds of distorted states of 4 patterns very well and brings the distorted patterns to stable equilibrium points. </br>
Below you can see how many iterations the network reaches stable equilibrium points. </br>
![image](https://user-images.githubusercontent.com/78887209/216769660-8ff8964a-e455-4a11-aa3a-9b75370e85a7.png) </br>
While training the network, it is aimed to use the data in this list to compare the data in this list with stable equilibrium points by assigning the x(k+1)==x(k) conditions to a list. Equilibrium points where some of the corrupted data converge can be seen below. </br>
![image](https://user-images.githubusercontent.com/78887209/216769723-f36449f3-0f61-4fa1-b171-0b34f3d7d8e2.png) ![image](https://user-images.githubusercontent.com/78887209/216769727-91f52be8-47ed-4c6d-ac72-995a60c0081d.png) </br>
Redundant memory has also occurred at some other points of convergence of corrupted data to the network, which will be discussed in the next section.
#### 3.Redundant Memory Status
In the discrete time hopfield network, 8 distorted images presented to the network reached 8 different stable equilibrium points. But in the case of x(k)==x(k+1) there are 12-14 different values on average that are assigned to the memory but do not converge to the stable equilibrium point. These values create redundant memory. Some data that makes up redundant memory can be seen below:
![image](https://user-images.githubusercontent.com/78887209/216769840-c20e9313-a8a2-4b45-b3c4-5402e221ed12.png) </br>
### Continuous Time Hopfield Network Associative Memory Design
#### 1.Creating the Memory
The Memory creation phase of the continuous time hopfield network is exactly the same as the discrete time hopfield network.
#### 2.Recall
The activation function was determined as tanh. Subsequently, the corrupted data was converted into a matrix (50.1) for ease of presentation to the network. You can see the name of this numpy array in the code as 'list_of_ilkkosul'. </br>
According to x(k+1) = x(k) * alpha + f(x(k)) * w condition, x(k+1) was found at each step. </br>
The stopping criterion for the data is that x(k+1) is equal to x(k). By adding the stopping criterion, the processes described above were applied to 8 corrupted data. </br>
The designed continuous-time associative hopfield network detects 8 patterns in total, including 2 types of distorted states of 4 patterns, and brings the distorted patterns to stable equilibrium points. Below you can see how many iterations the network reaches stable equilibrium points. </br>
![image](https://user-images.githubusercontent.com/78887209/216770535-5e7c91b3-0bdc-443d-ba1e-a24cf5ac10e9.png) </br>
While training the network, it is aimed to use the data in this list to compare the data in this list with stable equilibrium points by assigning the x(k+1)==x(k) conditions to a list. The size of the list is 1361, although all 8 patterns achieve stable equilibrium. This shows that there is quite a lot of redundant memory. </br>
#### 3.Redundant Memory Status
Below you can see some data that creates redundant memory. </br>
![image](https://user-images.githubusercontent.com/78887209/216770620-e726a50e-e971-4c89-9004-5cf1843d9fac.png)

