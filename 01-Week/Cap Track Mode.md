---
creation date: 2022-04-13 11:02
---

# Cap Track Mode
研究目标：自举开关模型在始终导通下的**电容分压行为**；

---


![[Pasted image 20220413222722.png]]

Vgs中存在**直流下降**以及**正弦纹波**：
- 纹波大小与G点**对地的寄生电容C_g**的大小有关；
- 直流下降取决于Cb电容放电，

---

## 0. 直线下降

![[Pasted image 20220414211213.png]]

 来自于Cb两端电荷流失，主要由两部分组成：
 1. 一部分是两端开关断开电阻依然在放电；
 2. 另一部分是MOS管的隧穿电流 **igs igd**；

仿真发现，其中隧穿电流占主导，依据：
1. 断开电阻从1T改为10T之后，观察两端电流大小发现，电流大小变为1/10，但是**Vgs的压降从1mV变化为700uV，不符合预期**；
2. 电容直连改成**VCVS连接**，Vgs的压降大幅度下降，同时改变断开电阻阻值，Vgs的压降变化**符合倍数关系**；

---

## 1. 正弦纹波

由于存在多个寄生电容的效应，因此考虑先用**VCVS隔断掉寄生电容对自举电容的影响，同时阻断了漏电流的对自举开关的放电行为**，人为地添加寄生电容，分析各个电容的影响。

以下的分析基于两点假设：
- 为简化计算，控制开关在 t = t\_dly 时刻打开，输入端在 t = 2t\_dly 时刻开始变化，从而保证计算时**每个节点的电压稳定且已知**；
- 电容的分压行为仅考虑与**栅极相连的三个电容**，即 G -> GND, G -> S, G -> D；

### 1.1 VCVS连接

当选择VCVS连接隔断掉MOS管的栅极与自举电容的上极板时，MOS管的寄生电容对自举电容分压行为的影响就可以忽略不记，此时需要**人为地添加电容**以实现对MOS管寄生电容的电容分压行为分析。

#### 1.1.1 Cp -> GND

首先考虑的是**栅极对地的总电容**，因为这一电容是在导通过程中对Vgs影响最大、最直观的一电容。

![[Pasted image 20220414223637.png]]

- 在开启之后( t > t\_dly)，由于Cp1 = Cb = 1 pF， 因此Vg0的电压变化满足：
$$\Delta V_{\text{g0}} = \frac{C_\text{p1}}{C_\text{t}} \Delta V_{\text{in}} = \frac{1}{2} \Delta V_{\text{in}}$$
- 在开启瞬间 ( t = t\_dly):

![[Pasted image 20220414224013.png]]

Cb上存储的电荷会发生**重分配**，从而使得Vg0电压发生变化，开启前后电荷满足：

$$
\left\{\begin{array}{l}
Q_{1}=C_{b} \times V_{D D} \\
Q_{2}=\left(V_{\text {cap0 }}-V_{\text {cm }}\right) \times C_{b}+V_{\text {cap0 }} \times C_{p} \\
Q_{1}=Q_{2}
\end{array} \quad \Rightarrow \quad V_{\text{cap0}}= \frac{C_b}{C_t}\left(V_{DD}+V_{\text{cm}}\right)\right.
$$

因此理论上Vcap0 = 1.35V，但是由于SW3与SW5在开启瞬间有**漏电流通过**，因此使得最终电容上机获得的电压仅为 1.335V。

![[Pasted image 20220414224452.png]]

#### 1.1.2 Cp -> S

其次考虑的是**栅极到输入端的寄生电容Cgs**，由于该电容是MOS管中容值较大的一个，对Vgs影响较大；

![[Pasted image 20220415011046.png]]

- 在开启之后( t > t\_dly)，由于自举电容的另一端**floating**，因此Vgs保持不变，即：
$$\Delta V_{\text{gs}} = 0$$
- 在开启瞬间 ( t = t\_dly):

![[Pasted image 20220415011637.png]]

在Cb电荷进行重分配的过程中，**栅极到输入端的寄生电容的表现与到地表现一致**，但仅是开启瞬间的；

$$
\left\{\begin{array}{l}
Q_{1}=V_{D D} \times C_{b}+\left(0-V_{c m}\right) \times C_{p 2} \\
Q_{2}=\left(V_{\text {capo }}-V_{c m}\right) \times\left(C_{b}+C_{p_{2}}\right) \\
Q_{1}=Q_{2}
\end{array} \quad \Rightarrow \quad V_{\text{cap0}}=\frac{C_{b}}{C_{t}} \times \left(V_{DD} + V_{cm} \right)\right.
$$

由于实际上MOS管的**Cgs会使得Cp2的容值增加**，使得仿真变得不准，计算后仿真与理论对的上。（Cp2 = 0.5 pF, Cgs = 120 fF -> Vgs = 0.76V）

#### 1.1.3 Cp -> D

此外，由于**栅极到输出端的寄生电容Cgd**大小与Cgs接近，但由于**输出端的电压不随着输入实时变化**，因此起对Vgs的贡献略有不同。

![[Pasted image 20220415133624.png]]

- 在开启瞬间 ( t = t\_dly):

![[Pasted image 20220415133816.png]]

由于在开启瞬间的，Vout有一个==初始电压${V_{out}(t_{dly})}$==，因此在电荷重分配时通过Cp3反映到栅极电压：

$$
\left\{\begin{array}{l}
Q_{1}=V_{DD} \times C_{b}+\left[0-V_{\text {out }}(t_{\text{dly}}) \right] C_{p3} \\
Q_{2}=\left(V_{\text {cap0 }}-V_{\text{cm}}\right) \times C_{b}+\left(V_{\text {cap0}}-{V_{\text {cm }}}\right) \times C_{p_{3}} \\
Q_{1}=Q_{2}
\end{array} \Rightarrow V_{\text {cap0 }}=V_{c m}+\frac{C_{b}}{C_t} V_{DD}-\frac{C_{p 3}}{C_{t}} V_{\text {out }}(t_{\text{dly}})\right.
$$

? 关于==初始电压${V_{out}(t_{dly})}$==的计算是个比较大的问题；

- 在开启之后( t > t\_dly)，由于Cp3是架在**栅极与输出点**之间的，会将ΔVds的部分电压反馈至栅极，即：

$$
\Delta V_{g 0}=-\frac{C_{p3}}{C_{b}+C_{p 3}} \cdot \Delta V_{d s}
$$

其中ΔVds 满足：

$$
\Delta V_{ds} = \left( R_{on} C_{L} \omega _{in} \right) \times\Delta V_{in} 
$$
![[Pasted image 20220415141241.png]]


### 1.2. 开关导通过程中的电容分压小结

从以上的分析可以看出，在开关导通过程中，对Vgs有影响的主要是 $C_{p (G \rightarrow GND)}$  与  $C_{p (G \rightarrow D)}$ ，而寄生到输入端的电容没有影响。


$$
\begin{array}{|c|c|c|}
\hline  
C_{\text{para}}   & \Delta V_{\text{gs}} & V_{\text{cap0}}\\

\hline 

C_{p (G \rightarrow S)} & 
- & 
\frac{C_b}{C_t}\left(V_{DD}+V_{\text{cm}}\right) \\

C_{p (G \rightarrow GND)} & 
\frac{C_{p (G \rightarrow GND)}}{C_t} \cdot \Delta V_{in} &
\frac{C_b}{C_t}\left(V_{DD}+V_{\text{cm}}\right) \\

C_{p (G \rightarrow D)} &
K \cdot \frac{C_{p (G \rightarrow D)}}{C_t} \cdot \Delta V_{in} & 
V_{c m}+\frac{C_{b}}{C_t} V_{DD}-\frac{C_{p 3}}{C_{t}} V_{\text {out }}(t_{\text{dly}})\\

\hline

\end{array}
$$

其中系数$K =  R_{on} C_{L} \omega _{in} << 1$，因此在导通的过程中，主要的影响因素在**栅极对地的寄生电容**。但是相较于导通过程中，**开启瞬间的电荷配分**我认为更值得考量，其幅值更大；

![[Pasted image 20220415150531.png]]



---

### ? 关于初始电压Vout的计算

在不使用下底板采样时, ${V_{out}(t_{dly})} = V_{out}(t_{dly} - t_{s})$, 其中 t_s 是采样周期，也就是说输出点电压保持不变，但此时 **charge injection** 无法消除。

![[Pasted image 20220415152222.png]]

当使用下底板采样时，最终采样电压有 $V_{out\_cap} = V_d - V_{d0}$ 保持，可以避免 **charge injection** ，但Vd点的电压计算成了一个问题。

![[Pasted image 20220415152633.png]]