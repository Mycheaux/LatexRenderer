# LatexRenderer
Latex renderer for google doc 

Ongoing project as a replacement for autolatex that will allow simple copy paste of latex eqn from your overleaf to gogle doc.

it reads everthing inside `\begin{equation}` and `\end{equation}`, no need to replace with `$$` . 

How to use and test? Google-doc > extention > add script > copy paste this code > deploy as test. 


example to try :

\begin{equation}
    \underset{\theta_m}{\operatorname{argmin}}(L(x-i \cdot m(x)) \land \underset{\theta_i}{\operatorname{argmin}}(L(y-m \cdot i(y)).
    \label{tandem_loss}
\end{equation}`
