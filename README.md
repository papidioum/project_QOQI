# project_QOQI
Project for Hackaton QHack 2023
# Estimating Ground State Energy of Molecules using VQE with Qiskit Estimator Primitive in Qiskit Runtime

###
Quantum computing is an exciting and rapidly developing field, but we are still some way from achieving the ideal, fault-tolerant quantum computer with enough depth to ensure the implementation of popular quantum algorithms like Quantum Phase Estimation (QPE) or Shor's algorithm. However, even in the era of Noisy Intermediate-Scale Quantum devices, it is still possible to leverage quantum algorithms to achieve quantum advantage in a range of problems. One such algorithm is the Variational Quantum Eigensolver (VQE), which uses variational principles to compute the ground state energy of a Hamiltonian. This has significant implications for quantum chemistry, as it allows for the study of molecular and material properties.

In this project, we aim to compute the ground state energy of the Beryllium Hydride (*BeH<sub>2*</sub>) molecule using the Estimator Primitive of Qiskit Runtime. This will enable me to leverage tools for Quantum Error Suppression and Mitigation, such as Dynamic Decoupling (DD) and Zero Noise Extrapolation (ZNE), in order to obtain the most accurate result possible. By comparing our results to those obtained in the literature, we can evaluate the effectiveness of these tools.

The *BeH<sub>2*</sub> molecule is of particular interest due to its linear and symmetric structure, allowing for the easy calculation of its properties , making it an attractive molecule to test the precision of the quantum algorithm. It also has a wide range of industrial applications such as the production of beryllium metal. However, it is also a toxic substance, highlighting the importance of proper handling. By accurately computing its ground state energy, we can gain a better understanding of its properties and how it behaves in different contexts.

This project represents an important step towards utilizing the power and precision of NISQ era quantum computing to better understand the properties of molecules and materials, and the potential applications of this technology in industry and beyond.
###





## Results

As we discussed previously, the reference value of -15.833396 hartrees is obtained at an interatomic distance of 1.333 Angstroms. We managed to essentially get decent values considering we used the qiskit 'ibmq_qasm_simulator'. First we started by using Brayvi-katar Mapper, we got a value of -15.39498 hartrees with computation time of 3h5mn.
![Brayvi Kitae mapper](https://user-images.githubusercontent.com/108539802/221980660-f84c4276-2112-4ec8-8802-c8062c88fddd.png)

We also managed to show that we obtained simular results (-15.39488 hartees) using Parity Mapper allowing to reduce the computation time by half using tow qubit reduction.

![Parity mapper](https://user-images.githubusercontent.com/108539802/221981479-34684b5e-edce-430f-a940-c921a29fe018.png)

We show below the comparison of our results.

![Comparison](https://user-images.githubusercontent.com/108539802/221981499-706ab654-1549-4906-a3f2-7111061e52ae.png)

## Future directions


