\chapter{SVM Problem}
\section{Concept}
What is the SVM? What is it useful for? What is the idea behind it?\\
\textit{answer}\\
The goal of this chapter is to use the Wolfe dual formulation of the SVM optimization problem in order to define it as a quadratic programming problem. In the following chapters, the problem will be solved using Interior-Point method and other algorithms.

\section{Hyperplane and Margin definition}
As already mentioned, the Support Vector Machine model use an hyperplane $H$ to compute the predictions with the aim of classifying the data in the correct class. In particular, $H$ is defined by a vector of parameters $w=w_1,w_2,...$ and a bias $b$. In fact, it can be written as $$H(x)=w^Tx+b=w_1x_1+w_2x_2+...+b$$

Note that $y$ is the vector that contains the labels corresponding to the class of each point. In the simplest formulation of the SVM, the points can be classified only in two different classes, represented by the label $+1$ for one class and $-1$ for the other. As a consequence, the vector $y$ containing the actual classes is $$y^T=[\pm1,\pm1,...]\Rightarrow y_i=\pm1$$.

The margin $M$ is the distance from the closest point $x_i$ of the dataset to the hyperplane $H$. It can be computed as $$M(x_i)=\frac{|w^Tx+b|}{||w||}$$

% maybe I should try to be more clear
The support vectors $x_{sv}$ are exactly those points on the margin, in other words the points (or point) closest to the hyperplane. To simplify the problem, it is possible to define a new hyperplane $\bar{H}$, where the new parameters with respect to the previous ones are $\bar{w}=\frac{w} {H(x_{sv})}$ and $\bar{b}=\frac{b}{H(x_{sv})}$. This allows to set the value of $\bar{H}(x_{sv})=1$. Note that these steps can be done WLOG (Without loss of generality). Now, the margin can be rewritten as $$M(x_{sv})=\frac{|\bar{w}^Tx+\bar{b}|}{||\bar{w}||}=\frac{1}{||\bar{w}||}$$

\section{Optimization problem}
The idea of the SVM model is to find the hyperplane $H$ that maximizes the margin M. The objective can function of the optimization problem therefore is $$\max_{w,b} M(x_{sv})\Rightarrow\max_{w,b}\frac{1}{||w||}\Rightarrow\min_{w,b}||w||\Rightarrow\min_{w,b}||w||^2$$

Now the constraint. In this basic formulation, misclassification is not allowed, for this reason, the actual class $y$ and the predicted class $\bar{y}$ using the hyperplane $H(x)=w^Tx+b$ must have the same sign. Note that $y_i=\pm1$ and $H(x)\geq1$, because $H$ was designed to have a minimum value of $1$ given by the support vectors. The constraint is then $$y\cdot\bar{y}\geq1\Rightarrow y\cdot(H(x))\geq1\Rightarrow y\cdot(w^Tx+b)\geq1$$

Together, the objective function and the constraint of what is called "Hard Margin SVM" is \begin{align*}
\text{min}_{w,b} \quad &||w||^2 \\
\text{s.t.} \quad &y_i\cdot(w^Tx_i+b)\geq1 \\
\end{align*}

\section{Soft Margin}
In the "Hard Margin SVM" just described, misclassification was not allowed. However, in real-world dataset, it can happen and it is important to allow a certain amount of it. The first change must be made in the constraint $$y_i\cdot(w^Tx_i+b)\geq1-\epsilon_i$$
The $\epsilon_i\geq0$ serves as a threshold to allow misclassification, because now $y$ and $\bar{y}$ can have different sign. Note that there is a different $\epsilon_i$ for each point. However, $\epsilon$ must be as small as possible and to reach this goal it is sufficient to add $\sum\epsilon_i$ in the objective function which is being minimized. Furthermore, a constant value $C$ can be added to change the impact of $\epsilon$ into the objective function. The final formulation of the "Soft Margin SVM" is \begin{align*}
\text{min}_{w,b} \quad &||w||^2 + C\sum_i^N\epsilon_i \\
\text{s.t.} \quad &y_i\cdot(w^Tx_i+b)\geq1-\epsilon_i \\
&\epsilon_i\geq0
\end{align*}

\section{Lagrangian and KKT Conditions}
% from wikipedia
For a convex optimization problem with inequality constraints \begin{align*}
\min_{x} \quad &f(x) \\
\text{s.t.} \quad &g_i(x)\leq0 \quad i=1,...,m
\end{align*} 

the Lagrangian Dual problem is \begin{align*}
\max_{u} \quad &\inf_x\bigg(f(x)+\sum_{j=1}^m u_j g_j(x) \bigg)\\
\text{s.t.} \quad &u_i\geq0 \quad j=1,...,m \\
\end{align*}

% more about wolfe dual problem
The Wolfe Dual problem in theory is 
\begin{align*}
\max_{x,u} \quad &f(x)+\sum_{j=1}^m u_j g_j(x) \\
\text{s.t.} \quad &\nabla f(x) + \sum_{j=1}^m u_j \nabla g_j(x)=0 \\
                &u_i\geq0 \quad i=1,...,m
\end{align*} 
% here maybe we should explain more theory
% for example why the duality gap is zero

The Lagrangian $\mathcal{L}$ of the primal formulation of the SVM problem can be written as \begin{align*}
\mathcal{L}(w,b,\epsilon,\alpha,\beta)=
\frac{||w||^2}{2} 
+ C\sum_i^m\epsilon_i 
- \sum_i^m\alpha_i\bigg(y_i(w^Tx_i+b)-(1-\epsilon)\bigg)
- \sum_i^m\beta_i(\epsilon_i)
\end{align*}

Note that the $\frac{1}{2}$ in the first term is added for convenience later with the derivative. The minus in the third and forth terms are needed because the original constraints must be multiplied by $-1$ in order to match with the form of the Lagrangian mentioned. $\alpha_i\geq0$ and $\beta_i\geq0$ are the Lagrangian multipliers.
\\ \\
% here maybe we should add a description of kkt
Using the KKT conditions, the Wolfe Dual problem can be obtained from the Lagrangian Dual problem. In particular, using the stationarity conditions to substitute $w$ and the complementary slackness conditions to obtain a maximization problem in terms of the dual variable $\alpha$.
\\ \\
The KKT conditions are...
\\
\\

With the appropriate rearrangements, it is possible to write some useful expressions from the KKT conditions:
$$\text{Stationarity Constraints} \\
\begin{cases}
    & w=\sum\alpha_i y_i x_i \\
    & 0=\sum\alpha_i y_i \\
    & C=\sum\alpha_i+\sum beta_i  \\
\end{cases}$$

$$\text{Complementary Slackness Constraints} \\
\begin{cases}
    & \alpha_i(y_i(x_i^Tw+b)-(1-\epsilon_i))=0 \\
    & \beta_i \epsilon_i =0
\end{cases}$$

Substituting these expressions into the Lagrangian $\mathcal{L}$:
\begin{align*}
\mathcal{L}&=\frac{||w||^2}{2} + C\sum_i^m\epsilon_i - \sum_i^m\alpha_i\bigg(y_i(w^Tx_i+b)-(1-\epsilon)\bigg) - sum_i^m\beta_i(\epsilon_i) \\
&=\frac{1}{2}\sum\sum\alpha_i\alpha_j y_i y_j x_i x_j - \sum\alpha_i y_i w^T x_i - \sum\alpha_i y_i b + \sum\alpha_i-\sum\alpha_i\epsilon_i + C\sum\epsilon_i - \sum\beta_i\epsilon_i \\
&=\frac{1}{2}\sum\sum\alpha_i\alpha_j y_i y_j x_i x_j - \sum\alpha_i y_i (\alpha_j y_j x_j) x_i - 0 + \sum\alpha_i - \sum\alpha_i\epsilon_i + \sum\alpha_i\epsilon_i + 0 - 0 \\
&=\frac{1}{2}\sum\sum\alpha_i\alpha_j y_i y_j x_i x_j - \sum\alpha_i\alpha_j y_i y_j x_i x_j + \sum\alpha_i \\
&=-\frac{1}{2}\sum\sum\alpha_i\alpha_j y_i y_j x_i x_j + \sum\alpha_i
\end{align*}

Recalling the Wolfe Dual problem, we can write the specific objective function for the SVM problem as
\begin{align*}
\max_{\alpha}\mathcal{L}(\alpha) \Rightarrow \min_{\alpha}-\mathcal{L}(\alpha) \Rightarrow \min_{\alpha}\frac{1}{2}\sum\sum\alpha_i\alpha_j y_i y_j x_i x_j - \sum\alpha_i
\end{align*}


\section{Dual formulation}