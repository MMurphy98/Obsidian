# Bootstrapped Switch

  

> used to model the distortion of Bootstrapped Switches and target to build a **high-speed low-distortion** Bootstrapped Switches.

  

## File Tree

  

### Model

  
  
  

- ✗ `Model_basic.m`: calculate the Id and Vout of the Bootstrapped Switches and model the **relationship of Ron and THD**; **first try**

  
  

- ✔︎`Id_getFR.m`: calculated the **frequency response of Id system**;

  

- ✔︎`getHD.m`: used the **linear equation group of Ron and HD** to calculate the  total distortion, with the variable fin and Ron, the function supportes the **vector** calculation;

  

- ✔︎`Model_DeltaRon.mlx`: analysis the relationship of Ron, Fin and HD, <- `getHD.m`;

  

  

### Simulink

  

- ✔︎`myr.scc`: basic model modified from the **variable resistor**;

  - **Input:** R (Ohm);

  - **Output:** Rout(Ohm) = Min{R_max, R};

- ✗ `Resistors.slx`, `Resistor_inverted.slx`: two simulation files of **myr.scc**;

- ✔︎`onSwitch.scc`: the MOSFET switch file modified from the **myr.scc**:

  - **Nodes**: 4 `electrical`, vp vn are used to sense the control voltage;

  - **Output:** Rout(Ohm) behavies like S D exchanged MOSFET;

- ✔︎`Boostrapped_Switch_v1.slx`,`Boostrapped_Switch_v2.slx`: the simulation files of **onSwitch.scc**

  - **Note:** the output signal is exported to the workspace to calculate the THD, by the file `Spectrum_Analysis.mlx`;

  -

  

## Archive

  

### [[001. Phase Order]]


  

### [[002. Bootstrapped Switches in  Simulink]]

  

**存储路径：** `~/Simulink`

  

**问题来源：** 在没有 Cadence Virtuoso 的情况下，利用 Simulink