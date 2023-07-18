
> **Approximation Lemma** ([[Oli15]], [[DSY09]]): Let $P(\mathbf{x}, y) \in \mathbb{F}[\mathbf{x}, y], P^{\prime}(\mathbf{x}, y) \equiv \frac{\partial P}{\partial y}(\mathbf{x}, y)$ and $\mu \in \mathbb{F}$ be such that $P(\mathbf{0}, \mu)=0$ but $P^{\prime}(\mathbf{0}, \mu)=\xi \neq 0$. Then, for each $t \geq 0$, there exists a unique polynomial $q_t(\mathbf{x})$ s.t. $\operatorname{deg}\left(q_t\right) \leq t, q_t(\mathbf{0})=\mu$ and $$
H_{\leq t}^{\mathbf{x}}\left[P\left(\mathbf{x}, q_t(\mathbf{x})\right)\right] \equiv 0
$$ Moreover, if $P$ can be computed by a formula (circuit) $\Gamma$ such that its output gate is an addition gate, there is a formula (circuit) $\Phi_t$ for the polynomial $q_t(\mathbf{x})$ such that the output gate of $\Phi_t$ is an addition gate, $$depth(\Phi_t)\leq depth(\Gamma)+2\text{ and } |\Phi_t|\leq 200(tr)^r{{t+r+1}\choose{r+1}}|\Gamma|$$

