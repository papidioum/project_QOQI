# project_QOQI
Project for Hackaton QHack 2023
# Estimating Ground State Energy of Molecules using VQE with Qiskit Estimator Primitive in Qiskit Runtime

###
Quantum computing is an exciting and rapidly developing field, but we are still some way from achieving the ideal, fault-tolerant quantum computer with enough depth to ensure the implementation of popular quantum algorithms like Quantum Phase Estimation (QPE) or Shor's algorithm. However, even in the era of Noisy Intermediate-Scale Quantum devices, it is still possible to leverage quantum algorithms to achieve quantum advantage in a range of problems. One such algorithm is the Variational Quantum Eigensolver (VQE), which uses variational principles to compute the ground state energy of a Hamiltonian. This has significant implications for quantum chemistry, as it allows for the study of molecular and material properties.

In this project, we aim to compute the ground state energy of the Beryllium Hydride (*BeH<sub>2*</sub>) molecule using the Estimator Primitive of Qiskit Runtime. This will enable me to leverage tools for Quantum Error Suppression and Mitigation, such as Dynamic Decoupling (DD) and Zero Noise Extrapolation (ZNE), in order to obtain the most accurate result possible. By comparing our results to those obtained in the literature, we can evaluate the effectiveness of these tools.

The *BeH<sub>2*</sub> molecule is of particular interest due to its linear and symmetric structure, allowing for the easy calculation of its properties , making it an attractive molecule to test the precision of the quantum algorithm. It also has a wide range of industrial applications such as the production of beryllium metal. However, it is also a toxic substance, highlighting the importance of proper handling. By accurately computing its ground state energy, we can gain a better understanding of its properties and how it behaves in different contexts.

This project represents an important step towards utilizing the power and precision of NISQ era quantum computing to better understand the properties of molecules and materials, and the potential applications of this technology in industry and beyond.

## Project implementation details

In this project, we aim to find the ground state energy of a molecular system using the variational quantum eigensolver (VQE) algorithm. The detailed implementation of our project can be found in the Jupyter Notebook.

To begin, we choose a molecular Hamiltonian in second quantization description to define the electronic structure of the molecule. In that description, the Hamiltonian is expressed in terms of fermionic creation and annihilation operators, corresponding to adding and removing electrons from an orbital basis. We select the most known linear and symmetric configuration of $BeH_2$ with an atomic distance $H-Be$ of $1.33$ Angstroms. In this configuration, the ground state energy of the molecule, computed in the $\textit{6-311G}$ basis, is $-15.83396$ Hartrees. We define our molecular geometry using cartesian coordinates centered at the Berylium atom (Be).

Next, we set a chemical driver associated with the charge and multiplicity of the molecule in a given basis. Multiplicity refers to the number of spin states that a molecule can adopt, and is defined as $2S + 1$, where $S$ is the total spin of the molecule. In the case of $BeH_2$, there are no unpaired electrons, as both valence electrons of the beryllium atom are involved in bonding. Its multiplicity is therefore $1$. We choose to compute the molecular structure problem in the $\textit{6-311G}$ basis, since the ground state reference value was computed in that basis.

$BeH_2$ consists of one beryllium atom and two hydrogen atoms. Beryllium has two valence electrons, which occupy the $2s$ atomic orbital. The two hydrogen atoms have one valence electron each, which occupy the $1s$ atomic orbital. When the Be and H atoms come together to form BeH2, their atomic orbitals overlap to create four molecular orbitals. To simulate the molecular orbitals with VQE, we select our active space using the $\textit{ActiveSpaceTransformer}$. This approach reduces computational cost by selecting important orbitals and electrons, rather than treating all orbitals and electrons with the same accuracy. We specify how many electrons and molecular orbitals we would like to have in our active space, as well as which particular orbitals we would like to consider.

We then create an ElectronicStructureProblem that produces a list of fermionic operators describing the fermionic Hamiltonian in the second quantization. Because electrons are fermions, electronic systems are described by Hamiltonians consisting of fermionic operators expressed in second quantization. Since quantum computers are made up of qubits, we transform such fermionic Hamiltonians into qubit operators using different fermionic to qubit operators mapper from Qiskit Runtime. We compare two different mappers, namely the $\textit{Brayvi-Kitae}$ method and the $\textit{Parity Mapper}$. The former minimizes the Pauli weight of the qubit Hamiltonian, which is generally referred to as the maximum number of qubits on which each Pauli string produced acts. The latter can use the $\textit{two qubit reduction}$ method to further reduce the number of required qubits and therefore the computational cost of the VQE operation. The two qubit reduction converter eliminates the central and last qubit in a list of Paulis that have diagonal operators (Z, I) in those positions. This is a useful method that can be used in chemistry problems to reduce computational resources.

Beyond this, we also generated a parametrised circuit (ansatz) based on the Hartree-Fock ground state as a trial state for our VQE routine.

In addition to the circuit optimization techniques discussed above, we also utilized Qiskit Runtime's built-in quantum error correction and mitigation tools, specifically the Estimator primitive with $\textit{options.optimization_level = 3}$. This optimization level employs the Dynamic Decoupling technique, which is designed to increase the lifetime of quantum information by disconnecting the environment during idle qubit states. By scanning the circuit for idle periods and inserting a DD sequence of gates during those times, the technique effectively mitigates decoherence without altering the logical action of the circuit. However, it is important to note that without an optimal decoupling sequence, the technique may not preserve qubit coherence.

To further improve error mitigation, we activated $\textit{options.resilience_level = 2}$, which applies the Digital Zero Noise Extrapolation (ZNE) technique. This popular technique mitigates errors in noisy quantum computers without requiring additional quantum resources. A quantum program is modified to run at different noise levels, and the result is extrapolated to an estimated value at a noiseless level. Digital ZNE scales noise using either analog or digital methods, but determining the best method is an active area of research. It is worth noting that the digital method does not affect the physical quantum pulses.




## Results

As we discussed previously, the reference value of -15.833396 hartrees is obtained at an interatomic distance of 1.333 Angstroms. We managed to essentially get decent values considering we used the qiskit 'ibmq_qasm_simulator'. First we started by using Brayvi-katar Mapper, we got a value of -15.39498 hartrees with computation time of 3h5mn.
![Brayvi Kitae mapper](https://user-images.githubusercontent.com/108539802/221980660-f84c4276-2112-4ec8-8802-c8062c88fddd.png)

We also managed to show that we obtained simular results (-15.39488 hartees) using Parity Mapper allowing to reduce the computation time by half using tow qubit reduction.

![Parity mapper](https://user-images.githubusercontent.com/108539802/221981479-34684b5e-edce-430f-a940-c921a29fe018.png)

We show below the comparison of our results.

![Comparison](https://user-images.githubusercontent.com/108539802/221981499-706ab654-1549-4906-a3f2-7111061e52ae.png)

## Future directions


