# Formula derivations

Here are formula derivations for paper "Enhance broadcasting throughput by associating network coding with UAVs relays deployment in emergency communications".

## Formula (6): The average number of transmissions under Protocol D

$$
\begin{aligned}
    E[&T_D\left(\{S_1,S_2,\cdots, S_n\},R, \{D_1,D_2,\cdots, D_m\} \right)] \\
    &
    \begin{aligned}
    = 1 &+ \sum_{\Delta}\bigg\lbrace
    \prod_{i\in [1,n]}\prod_{k\in [1,m]} (1-p_{(S_i,D_k)})^{\delta_{ik}}p_{(S_i,D_k)}^{(1-\delta_{ik})} \\
    &\times \bigg[
    \sum_{B}\Big(
    \prod_{j\in[1,n]} (1-p_{(S_j,R)})^{\beta_j} p_{(S_j,R)}^{(1-\beta_j)} \\
    &\times \big( (
    \sum_{z\in [1, |\mathbb{P}|]}(\mathbb{P}[z]-\mathbb{P}[z+1]) E[T_A(R,\mathbb{D}_{z})])+ E[T_D\left(\mathcal{S},R, \mathcal{D} \right)]
    \big) \Big) \bigg] \bigg\rbrace
    \end{aligned}        
\end{aligned}
$$

$p_{(S_i,D_k)}$ is the outage probability of source $S_i$ to destination  $D_k$ transmission which can be computed by Formula (1)  and (2).  In Step 1, $n$ sources broadcast $n$ packets, $m$ destinations have $2^{n\times m}$ possible  packet reception events. Each $\delta_{ik}$ is an indication function denoting whether $D_k$ has successfully received the packet from $S_i$ or not. $\delta_{xy}=1$ indicates that $D_y$ has successfully received the packet from $S_x$ in Step 1, otherwise $\delta_{xy}=0$. Obviously, $\prod_{i\in [1,n]}\prod_{k\in [1,m]} (1-p_{(S_i,D_k)})^{\delta_{ik}}p_{(S_i,D_k)}^{(1-\delta_{ik})}$ is the probability of a packet reception event for $m$ destinations after Step 1. 

$p_{(S_j,R)}$ is the outage probability of source $S_j$ to relay $R$ transmission which can be computed by Formula (1)  and (2). Similarly, there are $2^n$ possible  packet reception events for relay $R$ in Step 1. Each $\beta_{j}$ is an indication function denoting whether $R$ has successfully received the packet from $S_j$ or not. $\beta_{j}=1$ indicates that $R$ successfully received the packet from $S_j$ in Step 1, otherwise $\beta_{j}=0$. Obviously, $\prod_{j\in[1,n]} (1-p_{(S_j,R)})^{\beta_j} p_{(S_j,R)}^{(1-\beta_j)}$ s the probability of a packet reception event for the relay $R$ after Step 1. 

$$\sum_{z\in [1, |\mathbb{P}|]}(\mathbb{P}[z]-\mathbb{P}[z+1]) E[T_A(R,\mathbb{D}_{z})])$$ means the average number of transmissions in Step 2. $\mathbb{P}=\{p_{(S_x,D_y)}| (\beta_x = 1)\And (\delta_{xy}=0), \forall x\in [1,n], \forall y\in [1,m]\}$ is a set of outage probabilities arranged in descending order. $\mathbb{P}[z]$ means the $z$th element in set $\mathbb{P}$ and $\mathbb{P}[|\mathbb{P}|+1]=0$. $E[T_A(R,\mathbb{D}_z)]$ is the average number of transmissions from relay to destinations in $\mathbb{D}_z$ since all of them have failed receiving the packet from source $S_x$ when $\mathbb{P}[z]=p_{(S_x,D_y)}$. This is the same as the Formula (7) in [1].
$$
E[T_A(R,\mathbb{D}_z)] = \sum_{\Delta} \frac{(-1)^{1+\sum_{D_i\in \mathbb{D}_z}{\delta_i}}}{1-\prod_{D_i\in \mathbb{D}_z}{p_{(R,D_i)}^{\beta_i}}}
$$
$p_{(R,D_i)}$ is the outage probability of relay $R$ to destination  $D_i$ transmission which can be computed by Formula (1)  and (2). The derivation is same as Formula (15) in [2]. We assume the relay $R$ has successfully received the packet from $\{S_1,S_2,\cdots, S_n\}$, so $\mathbb{D}_z=\{D_1,D_2,\cdots, D_m\}$. After a sufficiently large number of transmissions $N$ from every source in $\{S_1,S_2,\cdots, S_n\}$, the numbers of lost packets at receivers $\{D_1,D_2,\cdots, D_m\}$ are $(Np_{(S_1,D_1)}, \cdots, Np_{(S_n,D_1)}), (Np_{(S_1,D_2)}, \cdots, Np_{(S_n,D_2)}), \cdots, (Np_{(S_1,D_m)}, \cdots, Np_{(S_n,D_m)})$, respectively. After sorting $p_{(S_1,D_1)}, \cdots,p_{(S_n,D_1)}, p_{(S_1,D_2)}, \cdots, p_{(S_n,D_2)}, \cdots, p_{(S_1,D_m)}, \cdots, p_{(S_n,D_m)}$ in ascending order, it becomes  $\mathbb{P}$. We can conceptually count the number of combinations for XORing the lost packets, and transmit these packets in different rounds. Therefore, the average number of transmissions that are required to successfully each source deliver all N packets to all the destinations is equal to
$$
N+N(\mathbb{P}[1]-\mathbb{P}[2])\phi_1+N(\mathbb{P}[2]-\mathbb{P}[3])\phi_1+N(\mathbb{P}[3]-\mathbb{P}[4])\phi_1+\cdots+N(\mathbb{P}[|\mathbb{P}|+1])\phi_{|\mathbb{P}|}
$$
where $\phi_i$ denotes the average number of transmissions that are required to successfully transmit a combined packet in round $i$. In our paper, this is  the average number of transmissions from relay to destinations.

$E[T_D\left(\mathcal{S},R, \mathcal{D} \right)]$ is a recursive component that represents the number of retransmissions required in the next iteration of Protocol D. Here, $\mathcal{S}=\{S_i|\forall i\in [1,n], \exists k\in [1,m], (\delta_{ik}=0)\&({\beta_i}=0)\}$ is a set of sources for which there exists at least one destination that has not successfully received the packet from this set after Steps 1 and 2. And $\mathcal{D}=\{D_k|\forall k\in [1,m], \exists i\in [1,n], (\delta_{ik}=0)\&({\beta_i}=0)\}$ is a set of destinations that have not received the packet from at least one source after Steps 1 and 2. 

## Formula (11): The average number of transmissions under Protocol B

We extend Protocol B into $n$-source $m$-destination broadcast transmissions by simply averaging the throughput of $n$ sources under Protocol B.
$$
E[T_B\left(\{S_1,S_2,\cdots, S_n\},R, \{D_1,D_2,\cdots, D_m\} \right)] = \frac{\sum_{i=1}^n{E[T_B\left(S_i,R, \{D_1,D_2,\cdots, D_m\} \right)]}}{n}
$$

$$
\begin{aligned}
	E[&T_B\left(S_i,R, \{D_1,D_2,\cdots, D_m\} \right)] \\
    &
    \begin{aligned}
    = 1 &+ \sum_{\Delta} \bigg\lbrace\prod_{k\in [1,m]} (1-p_{(S_i,D_k)})^{\delta_{ik}}p_{(S_i,D_k)}^{(1-\delta_{ik})} \\
    & \times \Big[ (1-p_{(S_i,R)})\times E[T_A\left(R,  \mathbb{D}\right)] \\
    &+ p_{(S_i,R)} \times E[T_B\left(S_i,R, \mathbb{D}\right)] \Big]\bigg\rbrace
    \end{aligned}
\end{aligned}
$$

The source $S_i$ broadcast $n$ packets, $m$ destinations have $2^{m}$ possible  packet reception events. Each $\delta_{ik}$ is an indication function denoting whether $D_k$ has successfully received the packet from $S_i$ or not. $\delta_{xy}=1$ indicates that $D_y$ has successfully received the packet from $S_x$. $\mathbb{D}=\{D_k|\delta_{ik}=0, \forall k\in[1,m]\}$ is a set of destinations that have not received the packet from source $S_i$. $E[T_B\left(S_i,R, \mathbb{D}\right)]$ is a recursive component that represents the number of retransmissions required in the next iteration of Protocol B.

Besides, since the broadcast throughput of Protocol B is also in recursive form and is hard to use, we use its lower bounds based on the same assumption that the UAV can successfully receive all packets from all BSs. In that case, the average number of transmissions is
$$
\begin{aligned}
    &E[T_B\left(\{S_1,S_2,\cdots, S_n\},R, \{D_1,D_2,\cdots, D_m\} \right)] \\
    &\begin{aligned}
    = 1 &+\frac{1}{n}\sum_{i\in [1,n]} \bigg\lbrace\sum_{\Delta}\prod_{k\in [1,m]}
    \Big[(1-p_{(S_i,D_k)})^{\delta_{ik}}p_{(S_i,D_k)}^{(1-\delta_{ik})} \\
    & \times {E[T_A(R,\mathbb{D})]}
    \Big]\bigg\rbrace
\end{aligned}
\end{aligned}
$$
When relay can successfully receive all packets from $\{S_1,S_2,\cdots, S_n\}$, we only have $E[T_A(R,\mathbb{D})]$ item no recursive  item.

## Reference

[1] P. Fan, C. Zhi, C. Wei, and K. B. Letaief, “Reliable relay assisted wireless multicast using network coding,” *IEEE Journal on Selected Areas in Communications*, vol. 27, no. 5, pp. 749–762, Jun. 2009, doi: [10.1109/JSAC.2009.090615](https://doi.org/10.1109/JSAC.2009.090615).

[2] D. Nguyen, T. Tran, T. Nguyen, and B. Bose, “Wireless Broadcast Using Network Coding,” *IEEE Transactions on Vehicular Technology*, vol. 58, no. 2, pp. 914–925, Feb. 2009, doi: [10.1109/TVT.2008.927729](https://doi.org/10.1109/TVT.2008.927729).
