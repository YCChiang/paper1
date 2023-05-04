# Formula derivations

Here are formula derivations for paper "Enhance broadcasting throughput by associating network coding with UAVs relays deployment in emergency communications".

## Formula (6): the average number of transmissions under Protocol D

$$
\begin{aligned}
    E[T_D&\left(\{S_1,S_2,\cdots, S_n\},R, \{D_1,D_2,\cdots, D_m\} \right)] \\
    &
    \begin{aligned}
    = 1 &+ \sum_{\Delta}\bigg\{ 
    \prod_{i\in [1,n]}\prod_{k\in [1,m]} (1-p_{(S_i,D_k)})^{\delta_{ik}}p_{(S_i,D_k)}^{(1-\delta_{ik})} \\
    &\times \bigg[
    \sum_{B}\Big(
    \prod_{j\in[1,n]} (1-p_{(S_j,R)})^{\beta_j} p_{(S_j,R)}^{(1-\beta_j)} \\
    &\times \big( (
    \sum_{z\in [1, |\mathbb{P}|]}(\mathbb{P}[z]-\mathbb{P}[z+1]) E[T_A(R,\mathbb{D}_{z})]) \\
    &+ E[T_D\left(\mathcal{S},R, \mathcal{D} \right)]
    \big) \Big) \bigg] \bigg\}
    \end{aligned}        
\end{aligned}
$$

Overall, the above formula is presented in recursive form. There are $2^{n\times m}$ possible transmitting-receiving events in total, and thus $|\Delta|=2^{n\times m}$  . For every event, the $RPN_e$ represents the number of retried packets. The constant 1 represents that any packet will transmit at least one time.
$\delta_{ik}$ is an indication function denoting whether $D_k$ has lost the packet broadcast by $S_i$ or not, that is, $\delta_{ik}=0$ means $D_k$ fails in receiving the packet, and $\delta_{ik}=1$ for the converse case. Obviously, $\prod_{i\in [1,n]}\prod_{k\in [1,m]}(1-p_{ik})^\delta_{ik}p_{ik}^{(1-\delta_{ik})}$ is the probability of an event in the first step of Protocol D. 

Similarly, there are $n$ possible relay receiving events, and thus $|B|=2^n$. $\beta_j$ is an indication function denoting whether the relay $R$ has lost the packet sent by $S_i$ or not. That is, $\beta_j=0$ means the relay has fails in receiving the packet sent by $S_i$, and $\beta_j=$ for the converse case. Obviously, $\prod_{j\in[1,n]} (1-\bar{p}_j)^\beta_j\bar{p}_j^{(1-\beta_j)}$ is the probability of one event in the second step of Protocol D.
% $\mathcal{S}=\{S_j|\beta_j=0\}$ is the set of sources whose packet broadcast in the first step has been received successfully by relay, and $\mathbb{D}_s=\{D_k|\delta_{sk}\}$ is the set of destinations that fail to receive the broadcast packet from the source $S_s$ in the first step. $E[T_A(R,\mathbb{D}_s)]$ is the average number of transmissions from relay to destinations in $\mathbb{D}_s$ since all of them have failed receiving the packet from source $S_s$. based on the formula (7) in \cite{fan_reliable_2009}, 

$$
E[T_A(R,\mathbb{D}_s)] = \sum_{\Delta}
 \frac{(-1)^{1+\sum_{i\in \mathbb{D}_s}{\delta_i}}}{1-\prod_{i\in \mathbb{D}_s}{\ddot{p}_i^{\beta_i}}}
$$

The term $\sum_{i=1}^{n\times m}(\vec{p}_i-\vec{p_{i-1}})\frac{\sum_{s\in \mathbb{S}}{E[T_A(R,\mathbb{D}_s)]}}{|\mathbb{S}|}$ is actually the number of transmissions in step two, which is indeed the formula (15) in \cite{nguyen_wireless_2009}. Note that it has great relation with the network coding-based relay strategy.

The term $E[T_D\left(\mathcal{S},R, \mathcal{D} \right)]$ is a recursive item which is the number of retry packets for delivering them to the destinations in the next loop executing Protocol D, where $\mathcal{S}=\{S_i|\exists k\in [1,m],(\delta_{ik}=0) \& ({\beta_i}=0)\}$, which includes all sources that failed their broadcasts, and $\mathcal{D}=\{D_k|\exists i\in [1,n],(\delta_{ik}=0) \& ({\beta_i}=0)\}$, which includes all destinations that failed their receiving.
