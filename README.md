\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage[total={6.5in,9in}]{geometry}

\title{MAT344 Learning Portfolio}
\author{Cheong Siu Lun, Chris}
\date{2022 Fall}

\usepackage{amsthm,amsmath,amssymb,amsfonts}
\usepackage{enumerate} 
\usepackage{hyperref}
\usepackage{tikz}
\newcommand{\Mod}[1]{\ \left(\mathrm{mod}\ #1\right)} 

\usepackage{tcolorbox} %create boxes
\usepackage{hyperref}
\hypersetup{colorlinks=true,
linkcolor=blue,
urlcolor=blue}
\usepackage{tree-dvips, qtree}
\usepackage[linguistics]{forest} %create tree diagrams
\usetikzlibrary{graphs}

\usetikzlibrary{angles,quotes} %notate angles
\usepackage{siunitx}
\usetikzlibrary{3d,calc} %create 3d objects
\usepackage{tikz-3dplot}
\usepackage{graphicx}

\tdplotsetmaincoords{60}{110}
\pgfmathsetmacro{\radius}{1} %Topic 1 Question 7 (hemisphere radius)
\pgfmathsetmacro{\thetavec}{0}
\pgfmathsetmacro{\phivec}{0}

\newtheorem{theorem}{Theorem}
\newtheorem{example}[theorem]{Example}

\usetikzlibrary[arrows.meta]
\newcommand{\rn}[2]{\tikz[remember picture,baseline=(#1.base)]\node [inner sep=0] (#1) {$#2$};}

\usepackage{tcolorbox} % Coloured boxes
\newtcolorbox{mybox}{colback=red!5!white,colframe=red!75!black}
\newtcolorbox{myboxb}{colback=blue!5!white,colframe=blue!75!black}
\newtcolorbox{myboxy}{colback=yellow!5!white,colframe=yellow!75!black}
\usepackage{tabularx} %for tables

\newcommand{\CC}{ \vfill 
\noindent{\tiny This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 2.5 Canada License. Author: Mike Pawliuk.} \includegraphics[scale=0.5]{CC.png} 
% This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 2.5 Canada License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/2.5/ca/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.
% Picture available at: https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-nc-sa.png
% This document was originally created by Micheal Pawliuk in Fall 2021 while he was a professor at the University of Toronto Mississauga (UTM).
% The materials were originally created for MAT344 Introduction to Combinatorics, a course at UTM.
}

\begin{document}

\maketitle

\section*{Introduction}
Combinatorics has always been an intimidating topic of Math for me, especially I have not taken any discrete math courses previously. I hope through this portfolio, I can achieve the following goals:

\begin{enumerate}
    \item Solve existing problems with different methods and create new conjectures (hopefully solving them)
    \item Apply combinatorics into my field of study, i.e. Financial Economics and Statistics
    \item Develop an analytical mindset
    \item Polish my coding skills, primarily \LaTeX \, and hopefully some Python and Matlab
\end{enumerate}
Therefore, in this portfolio, I would include the following content:
\begin{enumerate}
    \item Drafts and finalized solutions to problems from lectures and textbook
    \item Mistakes made in approaching the questions
    \item Concept points I learnt after correctly solving them
    \item Personal reflection on weekly journals
    \item Comprehensive questions of multiple fields of study
    \item Personal reflection on in-course growth and achievements
\end{enumerate}


\newpage
\section*{Table of Contents}
\begin{enumerate}
    \item Topic 1: Pigeonhole Principle
    \item Topic 2: Mathematical Induction
    \item Topic 3: Enumeration
    \item Journal Review
    \item Personal Reflection: Strength and Weakness
\end{enumerate}


\newpage
\section*{Topic 1: Pigeonhole Principle}

\begin{enumerate}[\bf(1)] %enumeration begins

\item (Question 1: The Jelly Beans Problem) %Question 1: Jelly Bean Problem
\begin{tcolorbox}[colback=blue!15]
Julia starts with an empty jar. Each day (for total days) Julia either puts one jelly bean in the jar or takes out one jelly bean and then records the total number of beans in the jar (to get a "jelly bean sequence" with 8 entries). At the end of the 8 days she has no jelly beans in the jar.\\\\
List out all possible jelly bean sequences.
\end{tcolorbox}

\textbf{Approach 1:} (Brute Force)\\
Since the number of days is 8 and eventually one has to yield 0 jelly in the jar at day 8, the maximum number of jellies one can get is 4 which will occur at day 4.\\\\
Secondly, the number of jellies at day 1, 7, and 8 are the same, which are 1, 1 and 0 respectively. Therefore, the variations will only occur at day 2 to day 6. Hence, we can simplify our tree diagram into 6 levels (days) as follow:

\begin{center}
\begin{forest}
[1[2[3[4[3[2]]][2[3[2]][1[2][0]]]][1[2[3[2]][1[2][0]]][0[1[2][0]]]]][0[1[2[3[2]][1[2][0]]][0[1[2][0]]]]]]
\end{forest}
\end{center}
As shown from the above tree diagram, we are able to solve this question by brute force. The number of branches at day 6 is 14, which means that there are \underline{\textit{\textbf{14}}} possible jelly bean sequences.\\\\
However, this method is tedious and time-consuming. Is there a smarter way to simplify the graph and even come up with a \textit{\textbf{general formula}} for the jelly bean problem for n number of days $(n \in \mathbb{Z}, n \ge 1)$?\\

\textbf{Approach 2}: (Lattice Path Method)\\
The following is another way of arranging the number of jelly beans in 8 days:
\begin{center}
    \begin{tikzpicture}[grow=right, nodes={circle,draw}]
    \node(a) at (-1,0) {1};
    \node(b) at (1,1) {0};
    \node(c) at (1,-1) {2};
    \node(d) at (3,0) {1};
    \node(e) at (3,-2) {3};
    \node(f) at (5,1) {0};
    \node(g) at (5,-1) {2};
    \node(h) at (5,-3) {4};
    \node(i) at (7,0) {1};
    \node(j) at (7,-2) {3};
    \node(k) at (9,1) {0};
    \node(l) at (9,-1) {2};
    \node(m) at (11,0) {1};
    \node(n) at (13,1) {0};
    \graph{(a) -> {(b),(c)} -> (d)};
    \graph{(c) -> (e)};
    \graph{{(d),(e)} -> (g)};
    \graph{(d) -> {(f),(g)} -> (i)};
    \graph{(e) -> {(g),(h)} -> (j)};
    \graph{{(i),(j)} -> (l)};
    \graph{(i) -> {(k),(l)} -> (m) -> (n)};
    \end{tikzpicture}
\end{center}
We can see the lattice path method is a neater way in presenting the change in number of jelly beans. We can also observe that there is a unique lattice pattern on each level. Then, the problem here is how to effectively count the number of paths one can take on the lattice structure, and how would the structure grow if $n>8$?

\item (Follow-up Question: The General Jelly Beans Problem) %General Jelly Bean Problem
\begin{tcolorbox}[colback=blue!15]
Again, Julia starts with an empty jar where she can either take one or add one jelly bean into the jar each day. However, this time she is planning to do this task for n days instead of 8 days. Therefore, for any $n \in \mathbb{Z}, n \ge 1$, what is the number of possible sequence where there is 0 beans left after n days?
\end{tcolorbox}
\textbf{Approach 1}: (Lattice Analysis)\\
\textit{Proof}\\
To analyze the pattern, let's start with some simple cases. Consider when $n=2,4,6$:\\
When $n=2$, the number of lattice paths is 1:
\begin{center}
    \begin{tikzpicture}[grow=right, nodes={circle,draw}]
    \node(a) at (-1,0) {1};
    \node(b) at (1,1) {0};
    \graph{(a)->(b)};
    \end{tikzpicture}
\end{center}
When $n=4$, the number of lattice paths is 2:
\begin{center}
    \begin{tikzpicture}[grow=right, nodes={circle,draw}]
    \node(a) at (-1,0) {1};
    \node(b) at (1,1) {0};
    \node(c) at (1,-1) {2};
    \node(d) at (3,0) {1};
    \node(e) at (5,1) {0};
    \graph{(a)->{(b),(c)}->(d)->(e)};
    \end{tikzpicture}
\end{center}
When $n=6$, the number of lattice paths is 5:
\begin{center}
    \begin{tikzpicture}[grow=right, nodes={circle,draw}]
    \node(a) at (-1,0) {1};
    \node(b) at (1,1) {0};
    \node(c) at (1,-1) {2};
    \node(d) at (3,0) {1};
    \node(e) at (5,1) {0};
    \node(f) at (3,-2) {3};
    \node(g) at (5, -1) {2};
    \node(h) at (7, 0) {1};
    \node(i) at (9,1) {0};
    \graph{(a)->{(b),(c)}->(d)->(e)};
    \graph{(c)->{(d),(f)}->(g)->(h)->(i)};
    \graph{(e)->(h)};
    \end{tikzpicture}
\end{center}
Here, we can notice there are several patterns going on:
\begin{enumerate}
    \item 0 jelly beans always occur on an even day, i.e. $n=2k$, $k \in \mathbb{N}$
    \item On the $n-1^{th}$ day where Julia obtains 1 jelly bean, the number of lattice paths passing through that node is the same as that on the $n^{th}$ day where she obtains 0 jelly bean.
    \item For every 2 days, the number of nodes increases by 1. e.g. at day 2, the number of nodes is 2; at day 4 the number of nodes is 3; and at day 6, the number of nodes is 4, etc.
\end{enumerate}
Hence, from (a), (b) and (c), we can generalize that the number of lattice paths that pass through a node equals to the sum of the number of paths of the previous 2 nodes. Therefore, if we replace the number of jelly beans inside the node with the number of lattice paths passing through individual nodes, we can obtain a graph as follow:
\begin{center}
    \begin{tikzpicture}[grow=right, nodes={circle,draw}]
    \node(a) at (-1,0) {0};
    \node(b) at (1,1) {1};
    \node(c) at (1,-1) {1};
    \node(d) at (3,0) {2};
    \node(e) at (3,-2) {1};
    \node(f) at (5,1) {2};
    \node(g) at (5,-1) {3};
    \node(h) at (5,-3) {1};
    \node(i) at (7,0) {5};
    \node(j) at (7,-2) {4};
    \node(k) at (9,1) {5};
    \node(l) at (9,-1) {9};
    \node(m) at (11,0) {14};
    \node(n) at (13,1) {14};
    \graph{(a) -> {(b),(c)} -> (d)};
    \graph{(c) -> (e)};
    \graph{{(d),(e)} -> (g)};
    \graph{(d) -> {(f),(g)} -> (i)};
    \graph{(e) -> {(g),(h)} -> (j)};
    \graph{{(i),(j)} -> (l)};
    \graph{(i) -> {(k),(l)} -> (m) -> (n)};
    \end{tikzpicture}
\end{center}
Interestingly, after we have written the nodes in this format, if we view the nodes vertically by each day, the sum of the nodes on each day equals to $\binom{i}{n_{i}-1}$ where i is the number of days and $n_{i}$ refers to the number of nodes of day i. For example, at day 12, the number of nodes is 7. Therefore, the sum of nodes on day 12 is $\binom{12}{7-1}=\textbf{924}=132+297+275+154+54+11+1$.
\begin{center}
    \begin{tikzpicture}[grow=right]
    \node[circle,draw](a1) at (-1,0) {0};
    \node[circle,draw](b1) at (0,1) {1};
    \node[circle,draw](b2) at (0,-1) {1};
    \node(bfuncion) at (0,-1.72) {$\binom{2}{1}=2$};
    \node[circle,draw](c1) at (1,0) {2};
    \node[circle,draw](c2) at (1,-2) {1};
    \node(cfuncion) at (1,-2.72) {$\binom{3}{1}=3$};
    \node[circle,draw](d1) at (2,1) {2};
    \node[circle,draw](d2) at (2,-1) {3};
    \node[circle,draw](d3) at (2,-3) {1};
    \node(dfuncion) at (2,-3.72) {$\binom{4}{2}=6$};
    \node[circle,draw](e1) at (3,0) {5};
    \node[circle,draw](e2) at (3,-2) {4};
    \node[circle,draw](e3) at (3,-4) {1};
    \node(efuncion) at (3,-4.72) {$\binom{5}{2}=10$};
    \node[circle,draw](f1) at (4,1) {5};
    \node[circle,draw](f2) at (4,-1) {9};
    \node[circle,draw](f3) at (4,-3) {5};
    \node[circle,draw](f4) at (4,-5) {1};
    \node(ffuncion) at (4,-5.72) {$\binom{6}{3}=20$};
    \node[circle,draw](g1) at (5,0) {14};
    \node[circle,draw](g2) at (5,-2) {14};
    \node[circle,draw](g3) at (5,-4) {6};
    \node[circle,draw](g4) at (5,-6) {1};
    \node(gfuncion) at (5,-6.72) {$\binom{7}{3}=35$};
    \node[circle,draw](h1) at (6,1) {14};
    \node[circle,draw](h2) at (6,-1) {28};
    \node[circle,draw](h3) at (6,-3) {20};
    \node[circle,draw](h4) at (6,-5) {7};
    \node[circle,draw](h5) at (6,-7) {1};
    \node(hfuncion) at (6,-7.72) {$\binom{8}{4}=70$};
    \node[circle,draw](i1) at (7,0) {42};
    \node[circle,draw](i2) at (7,-2) {48};
    \node[circle,draw](i3) at (7,-4) {27};
    \node[circle,draw](i4) at (7,-6) {8};
    \node[circle,draw](i5) at (7,-8) {1};
    \node(ifuncion) at (7,-8.72) {$\binom{9}{4}=126$};
    \node[circle,draw](j1) at (8,1) {42};
    \node[circle,draw](j2) at (8,-1) {90};
    \node[circle,draw](j3) at (8,-3) {75};
    \node[circle,draw](j4) at (8,-5) {35};
    \node[circle,draw](j5) at (8,-7) {9};
    \node[circle,draw](j6) at (8,-9) {1};
    \node(jfuncion) at (8,-9.72) {$\binom{10}{5}=252$};
    \node[circle,draw](k1) at (9,0) {132};
    \node[circle,draw](k2) at (9,-2) {165};
    \node[circle,draw](k3) at (9,-4) {110};
    \node[circle,draw](k4) at (9,-6) {44};
    \node[circle,draw](k5) at (9,-8) {10};
    \node[circle,draw](k6) at (9,-10) {1};
    \node(kfuncion) at (9,-10.72) {$\binom{11}{5}=462$};
    \node[circle,draw](l1) at (10,1) {132};
    \node[circle,draw](l2) at (10,-1) {297};
    \node[circle,draw](l3) at (10,-3) {275};
    \node[circle,draw](l4) at (10,-5) {154};
    \node[circle,draw](l5) at (10,-7) {54};
    \node[circle,draw](l6) at (10,-9) {11};
    \node[circle,draw](l7) at (10,-11) {1};
    \node(lfuncion) at (10,-11.72) {$\binom{12}{6}=924$};
    \node[circle,draw](m1) at (11,0) {429};
    \node[circle,draw](m2) at (11,-2) {572};
    \node[circle,draw](m3) at (11,-4) {429};
    \node[circle,draw](m4) at (11,-6) {208};
    \node[circle,draw](m5) at (11,-8) {65};
    \node[circle,draw](m6) at (11,-10) {12};
    \node[circle,draw](m7) at (11,-12) {1};
    \node(mfuncion) at (11,-12.72) {$\binom{13}{6}=1716$};
    \graph{(a1)->(b1)};
    \graph{(b2)->(c1)->(d1)};
    \graph{(c2)->(d2)->(e1)->(f1)};
    \graph{(d3)->(e2)->(f2)->(g1)->(h1)};
    \graph{(e3)->(f3)->(g2)->(h2)->(i1)->(j1)};
    \graph{(f4)->(g3)->(h3)->(i2)->(j2)->(k1)->(l1)};
    \graph{(g4)->(h4)->(i3)->(j3)->(k2)->(l2)->(m1)};
    \graph{(h5)->(i4)->(j4)->(k3)->(l3)->(m2)};
    \graph{(i5)->(j5)->(k4)->(l4)->(m3)};
    \graph{(j6)->(k5)->(l5)->(m4)};
    \graph{(k6)->(l6)->(m5)};
    \graph{(l7)->(m6)};
    \graph{(a1)->(b2)->(c2)->(d3)->(e3)->(f4)->(g4)->(h5)->(i5)->(j6)->(k6)->(l7)->(m7)};
    \graph{(b1)->(c1)->(d2)->(e2)->(f3)->(g3)->(h4)->(i4)->(j5)->(k5)->(l6)->(m6)};
    \graph{(d1)->(e1)->(f2)->(g2)->(h3)->(i3)->(j4)->(k4)->(l5)->(m5)};
    \graph{(f1)->(g1)->(h2)->(i2)->(j3)->(k3)->(l4)->(m4)};
    \graph{(h1)->(i1)->(j2)->(k2)->(l3)->(m3)};
    \graph{(j1)->(k1)->(l2)->(m2)};
    \graph{(l1)->(m1)};
    \end{tikzpicture}
\end{center}
Hence, we can deduce the general formula for the sum of lattice paths on an individual day i ($S_{i}$) is:
$$
S_{i}=\binom{i}{n_{i}-1} \text{ where } n_{i}=\begin{cases} \frac{i}{2}+1 \text{ for } i=2k \text{, } k \in \mathbb{N} \cup \{0\}\\
\frac{i+1}{2} \text{ for } i=2k+1 \text{, } k \in \mathbb{N}\symbol{92}\{1\} 
\end{cases}
$$
Strangely, another graphical interpretation of the sum of lattice columns can be observed from the Pascal's Triangle:
\begin{center}
    \begin{tikzpicture}[grow=down, nodes={circle,draw}]
    \node(a1) at (0,0) {1};
    \node(b1) at (-1,-1) {1};
    \node(b2) at (1,-1) {1};
    \node(c1) at (-2,-2) {1};
    \node(c2) at (0,-2) {2};
    \node(c3) at (2,-2) {1};
    \node(d1) at (-3,-3) {1};
    \node(d2) at (-1,-3) {3};
    \node(d3) at (1,-3) {3};
    \node(d4) at (3,-3) {1};
    \node(e1) at (-4,-4) {1};
    \node(e2) at (-2,-4) {4};
    \node(e3) at (0,-4) {6};
    \node(e4) at (2,-4) {4};
    \node(e5) at (4,-4) {1};
    \node(f1) at (-5,-5) {1};
    \node(f2) at (-3,-5) {5};
    \node(f3) at (-1,-5) {10};
    \node(f4) at (1,-5) {10};
    \node(f5) at (3,-5) {5};
    \node(f6) at (5,-5) {1};
    \node(g1) at (-6,-6) {1};
    \node(g2) at (-4,-6) {6};
    \node(g3) at (-2,-6) {15};
    \node(g4) at (0,-6) {20};
    \node(g5) at (2,-6) {15};
    \node(g6) at (4,-6) {6};
    \node(g7) at (6,-6) {1};
    \graph{(b1)->(c2)->(d2)->(e3)->(f3)->(g4)};
    \end{tikzpicture}
\end{center}
We can see that the lattice sums of each day i appears to be a zig-zag pattern on the Pascal's Triangle. However, the combinatorial argument for such relationship to exist is difficult to be proven.\\
Now, going back to finding the general formula for having 0 beans after n days. Since, we notice that the possible days of obtaining 0 beans are even days, i.e. day 2, 4, 6, 8, etc. and the sum of lattice paths $S_i$ for each of the day is 2, 6, 20, 70 respectively; while the number of possible sequence $n_i$ is 1, 2, 5, 14, etc. By listing them out on a table, we can see that:
\begin{center}
\begin{tabular}{c c c c c c c}
\textbf{i}:&2&4&6&8&10&12\\
\textbf{$S_i$}:&2&6&20&70&252&924\\
\textbf{$n_i$}:&1&2&5&14&42&132\\
\textbf{$\frac{S_i}{n_i}$}:&2&3&4&5&6&7
\end{tabular}
\end{center}
Hence, the general formula in terms of day i is:
$$n_i=\frac{S_i}{\frac{i}{2}+1}=\frac{2S_i}{i+2}$$
For clarity, we now re-denote the variables again so as to be in line with the question, i.e. number of days = N, sum of nodes of a specific day N = $S_N$, number of lattice paths on an individual node = $n_N$, and number of possible sequence of that day = f(N):
$$f(N)=\frac{2S_N}{N+2} \text{ in which}$$
$$S_{N}=\binom{N}{n_{N}-1} \text{ where } n_{N}=\begin{cases} \frac{N}{2}+1 \text{ for } N=2k \text{, } k \in \mathbb{N} \cup \{0\}\\
\frac{N+1}{2} \text{ for } N=2k+1 \text{, } k \in \mathbb{N}\symbol{92}\{1\} 
\end{cases}$$
Since we can only obtain 0 jellybeans at an even number of days, i.e. $N=2k$ for $k \in \mathbb{N}\symbol{92}\{0\}$, hence we can simplify the above equation by substituting $n=\frac{N}{2}+1$. Hence, the general formula for $f(N)$ is
$$f(N)=\frac{2\binom{N}{\frac{N}{2}}}{N+2} \text{ for } N=2k,k \in \mathbb{N}\symbol{92}\{0\}$$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
This method is able to generalize into a formula of N, i.e. the number of days, however, it still somehow feels cumbersome and one begs a question: Is there another simpler way to represent the jellybean conjecture? And in fact, there is! And it utilizes the method of generating functions.\\



\textbf{Approach 2}: (Generating Functions/The Catalan Numbers)\\
\textit{Proof}\\
Let $\{c_n\}_{n\geq0}$ be a sequence of jellybeans such that after $2n$ days where $n\in \mathbb{N}$, the number of jellybeans in the jar is 0, i.e. $c_n$ is the cardinality of sequences S such that $S_i=\{b_1,b_2,\ldots,b_{2n}\}$ where $b_j=\pm1 \text{, for all } j$, with $\sum_{j=1}^{2n}b_j=0 \text{ for all } k \in [2n]$. Then the formal power series/generating function is
$$C(x)=\sum_{n\geq0}c_nx^n$$
Since we have proven in approach 1 (lattice path approach) that 0 jellybeans can only be obtained on an even day, suppose there exists day $2i$ which is the first day when 0 jellybeans is obtained, then the jellybean sequence from $2i$ to $2n$ is equivalent to another valid jellybean sequence of length $2(n-i)$, for example at day 6, one valid sequence is $0-1-0-1-2-1-0 \iff \{+1,-1,+1,+1,-1,-1\}$. Since 0 is already obtained at day 2 with sequence $0-1-0$, hence the remaining sequence is equivalent to a sequence in day 4, i.e. $0-1-2-1-0$. This implies that we can break up the 2n days into 2 sequences:
\begin{enumerate}
    \item From 0 to 2i
    \item From 2i to 2n
\end{enumerate}
For the first 2i days, the sequence has all positive partial sums $\sum_{j=1}^kb_j$ if $0<k<2i$. Since the sequence $\{b_1,b_2,\ldots,b_{2i}\}$ is bijective with $\{b_2,b_3,\dots,b_{2i-1}\}$, removing the first and last entries, i.e. $b_1$ and $b_{2i}$, would still imply that $\sum_{i=2}^{2i-1}b_i\geq0$. Therefore, we can see that
$$|S_i|=c_{i-1} \Rightarrow \sum_{n\geq1}c_{n-1}x^n=x\sum_{n\geq1}c_{n-1}x^{n-1}=xC(x)$$
Therefore, by the Product Formula, i.e. $A(x)B(x)=C(x)$, we can see that
$$c_0=1$$
$$c_{n+1}=\sum_{i=0}^nc_i\cdot c_{n-i}$$
By applying the method of generating functions, we can see that
$$\sum_{n\geq0}c_{n+1}x^{n+1}=\sum_{n\geq0}x^{n+1}(\sum_{i=0}^nc_i\cdot c_{n-i})$$
$$\sum_{n\geq0}c_{n}x^{n}-c_0x^0=x\sum_{n\geq0}(\sum_{i=0}^nc_ix^i\cdot c_{n-i}x^{n-i})$$
For L.H.S., we notice that it is missing the term $c_0x^0$ such that it becomes $C(x)$. Therefore, it can be written as
$$C(x)-1=xC(x)\cdot C(x)$$
Rewriting the above equation, it will give us
$$xC(x)^2-C(x)+1=0$$
Since the above equation is quadratic, by $x=\frac{-b \pm \sqrt{b^2-4ac}}{2a}$, we can see that $C(x)$ has 2 solutions
$$C(x)=\frac{1+\sqrt{1-4x}}{2x} \text{ or } \frac{1-\sqrt{1-4x}}{2x}$$
By substituting $x=0$, we can see the second solution satisfies the property of $C(0)=1$. Hence, after some simplifications, we can see
$$C(x)=\sum_{n\geq0}\frac{\binom{2n}{n}}{n+1}x^n$$
Therefore, we can see that
$$c_n=\frac{\binom{2n}{n}}{n+1}$$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
The difficulty of this solution in my opinion is to understand how the jellybean sequence is a product of 2 smaller jellybean sequence (generating functions). Another tricky part is to realize that we can decompose the $x^{n+1}$ in the generating function into $x$, $x^i$, and $x^{n-i}$ such that the latter 2 generating functions in R.H.S. can have a closed form. After that, we are pretty much done can can obtain a closed form for the jellybean conjecture. One question that still lies here is whether the proof in approach 1 and this approach are equivalent? And if so, how to prove it combinatorially?



\item (Follow-up Question: Jellybean Combinatorial Proof)
\begin{tcolorbox}[colback=blue!15]
From approach 1 (lattice method) and approach 2 (generating functions) above, we seem to obtain the same results by plugging numbers into n in both closed-form functions. Prove combinatorially that $f_n \equiv c_n$, i.e.
$$\frac{2\binom{n}{\frac{n}{2}}}{n+2} \equiv \frac{\binom{2n}{n}}{n+1}$$
\end{tcolorbox}




\newpage
\item (Question 4: Textbook Question 1.17)
\begin{tcolorbox}[colback=blue!15]
Let A be an $n \times n$ matrix with 0 and 1 entries only. Let us assume that $n \ge 2$, and that at least $2n$ entries are equal to 1. Prove that A contains two entries equal to 1 so that one of them is strictly above and strictly on the right of the other.
\end{tcolorbox}
\textit{Proof}
\begin{enumerate}
    \item Consider the base case, when $n = 2$, A is a $2 \times 2$ matrix. Therefore, there are $2(2) = 4$ entries that are equal to 1, i.e.
    $$\begin{pmatrix}
    1 & \color{red}\boxed{1}\\1 & 1
    \end{pmatrix}$$\\
    Since entry $a_{1,2}$ is diagonal to entry $a_{2,1}$, there is an entry that is strictly above and on the right of another. Hence, the base case holds.
    \item Let $n=k$ such that $\exists k \in \mathbb{N}, k \ge 2$, a $k \times k$ matrix has at least 2k entries equal to 1 $\Rightarrow$ the matrix contains at least 2 entries equal to 1 so that one of them is strictly above and strictly on the right of the other. (By Induction Hypothesis)\\
    If $n=k+1$, we will have to prove that a $k+1 \times k+1$ matrix has $2k+2$ entries equal to 1 $\Rightarrow$ the matrix contains at least 2 entries equal to 1 so that one of them is strictly above and strictly on the right of the other. Therefore, consider the following $k+1 \times k+1$ matrix:
    $$\begin{pmatrix}
    \color{red}a_{1,1} & a_{1,2} & \color{red}a_{1,3} & \cdots & a_{1,k-1} & \color{red}a_{1,k} & a_{1,k+1}\\
    a_{2,1} & \color{red}a_{2,2} & a_{2,3} & \cdots & \color{red}a_{2,k-1} & a_{2,k} & \color{red}a_{2,k+1}\\
    \color{red}a_{3,1} & a_{3,2} & \color{red}a_{3,3} & \cdots & a_{3,k-1} & \color{red}a_{3,k} & a_{3,k+1}\\
    \vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots\\
    a_{k-1,1} & \color{red}a_{k-1,2} & a_{k-1,3} & \cdots & \color{red}a_{k-1,k-1} & a_{k-1,k} & \color{red}a_{k-1,k+1}\\
    \color{red}a_{k,1} & a_{k,2} & \color{red}a_{k,3} & \cdots & a_{k,k-1} & \color{red}a_{k,k} & a_{k,k+1}\\
    a_{k+1,1} & \color{red}a_{k+1,2} & a_{k+1,3} & \cdots & \color{red}a_{k+1,k-1} & a_{k+1,k} & \color{red}a_{k+1,k+1}\\
    \end{pmatrix}$$
    From the above matrix, we are able to divide the matrix into diagonals classified by the sum of the indexes of the entries (i.e. \textit{i} and \textit{j} of $a_{\textit{i},\textit{j}}$). If 2 entries have the same index sum $\textit{i}+\textit{j}$, then they are in the same diagonal (indicated by the alternating red-and-white entries).\\
    Here, by the pigeonhole principle, the pigeonholes are the entries in the lower-left corner of each diagonal (underlined). 
    $k+1 \times k+1$ matrix:
    $$\begin{pmatrix}
    \underline{\color{red}a_{1,1}} & a_{1,2} & \color{red}a_{1,3} & \cdots & a_{1,k-1} & \color{red}a_{1,k} & a_{1,k+1}\\
    \underline{a_{2,1}} & \color{red}a_{2,2} & a_{2,3} & \cdots & \color{red}a_{2,k-1} & a_{2,k} & \color{red}a_{2,k+1}\\
    \underline{\color{red}a_{3,1}} & a_{3,2} & \color{red}a_{3,3} & \cdots & a_{3,k-1} & \color{red}a_{3,k} & a_{3,k+1}\\
    \underline{\vdots} & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots\\
    \underline{a_{k-1,1}} & \color{red}a_{k-1,2} & a_{k-1,3} & \cdots & \color{red}a_{k-1,k-1} & a_{k-1,k} & \color{red}a_{k-1,k+1}\\
    \underline{\color{red}a_{k,1}} & a_{k,2} & \color{red}a_{k,3} & \cdots & a_{k,k-1} & \color{red}a_{k,k} & a_{k,k+1}\\
    \underline{a_{k+1,1}} & \underline{\color{red}a_{k+1,2}} & \underline{a_{k+1,3}} & \underline{\cdots} & \underline{\color{red}a_{k+1,k-1}} & \underline{a_{k+1,k}} & \underline{\color{red}a_{k+1,k+1}}\\
    \end{pmatrix}$$
    Here, we notice that the number of entries on the "L-shape" is
    $$k+1+k=2k+1$$
    Since there are $2k+2$ pigeons, there must be a diagonal that consists at least more than 1 entries, which means the original statement holds.
    \begin{flushright}
    $\square$
    \end{flushright}
\textit{Remark}:\\
In the textbook, this question is solved simply with the Pigeonhole Principle without induction. I think for a complete proof, M.I. is necessary as we are asked to prove a general case involving a variable n where $n \in \mathbb{R}, n \ge 2$. This question has taught me in order to approach Pigeonhole Principle, we need to identify the pigeonhole and the pigeons, as well as discovering a way to partition the region fairly. Also, this question has put my coding skills into test, especially when coding up the $k+1 \times k+1$ matrices.
\end{enumerate}


\newpage
\item (Question 5: Textbook Question 1.21)
\begin{tcolorbox}[colback=blue!15]
A group of seven co-workers are trying to predict the total number of points scored in a given basketball game. The first six people already took their guesses, and curiously, they all picked distinct even numbers. Mr. Slow is the last person to guess, and he knows all previous guesses. Is there a strategy for him that his guess will be better than the guesses of half of his colleagues?
\end{tcolorbox}
\textbf{Approach 1:} (Taking Average)\\
Yes, there is a strategy and the strategy is that Mr. Slow should give the average number of the previous 6 guesses in order to be better off than half of his colleagues.\\
\textit{Proof}\\
Since the 6 guesses are distinct even numbers, we can denote
the set of guesses as $$A=\{2k_{1},2k_{2},2k_{3},2k_{4},2k_{5},2k_{6}\}$$
Then the average is 
$$\bar{x}=\frac{2k_{1}+2k_{2}+2k_{3}+2k_{4}+2k_{5}+2k_{6}}{6}=\frac{k_{1}+k_{2}+k_{3}+k_{4}+k_{5}+k_{6}}{3} \in \mathbb{R}^{+} \symbol{92} \{2n \text{, } \forall n \in \mathbb{N}\} $$
Since $\bar{x}$ is an odd number, then $\bar{x} \notin A$. Therefore, a number line with 7 distinct elements can be drawn, where there are 3 elements to the both the right and left of $\bar{x}$.\\
Hence, if the real score $x_{real}$ is greater than $\bar{x}$, then $\bar{x}$ is a better guess than $\{2k_{1},2k_{2},2k_{3}\}$. By symmetry, if $x_{real}$ is smaller than $\bar{x}$, then then $\bar{x}$ is a better guess than $\{2k_{4},2k_{5},2k_{6}\}$.
\begin{flushright}
$\square$
\end{flushright}
\textit{Remark}:\\
Although this method seems solid, this method fails when there are extreme values in guesses. For example, let's consider the following set
$$A = \{2,4,6,8,10,100\}$$
The mean $\bar{x} \approx 21.67$, thus if the set is ordered
$$\{\underbrace{2,4,6,8,10}_{5 \text{ elements}},\textbf{21.67},100\}$$
Then there is an unequal number of elements on both sides of $\hat{x}$. If $x_{real}$ lies on the left of $\hat{x}$, then Mr. Slow's average-taking method will not make him better than half of his colleagues.\\
Therefore, we need to formulate another strategy for Mr. Slow to guarantee his success.\\\\

\textbf{Approach 2:} (Taking Median)\\
Denote Mr. Slow's median guess as $\hat{x}$, then the set of all guesses will be
$$\{\underbrace{2k_{1},2k_{2},2k_{3}}_{3 \text{ elements}},\hat{x},\underbrace{2k_{4},2k_{5},2k_{6}}_{3 \text{ elements}}\}$$
If $x_{real} \ge \hat{x}$, the $\hat{x}$ will always be closer to $x_{real}$ than the first 3 elements. By symmetry, if $x_{real} \leq \hat{x}$, the $\hat{x}$ will always be closer to $x_{real}$ than the latter 3 elements.
\begin{flushright}
$\square$
\end{flushright}

\newpage
\item (Follow-up Questions: The General Guessing Strategy)
\begin{tcolorbox}[colback=blue!15]
\begin{enumerate}
    \item Now, instead of 6 colleagues, Mr. Slow has n colleagues $(n \in \mathbb{N})$. Is it still possible for him to have a winning strategy?
    \item On top of n colleagues, his colleagues now are guessing distinct positive integers. Is there still a winning strategy for him?
    \item If Mr. Slow's colleagues are now guessing distinct positive integers, is there a strategy that he can guess better than 60\% of his colleagues? And what is the smallest number of n?
    \item The colleagues are still guessing distinct positive integers. Now, Mr. Slow is getting faster in guessing and he is no longer the last person to guess. Is there a way that he can guess better than half of his colleagues without knowing everyone's guesses? And what is the smallest number of colleague's guesses he need to know?
\end{enumerate}
\end{tcolorbox}
\begin{enumerate}
    \item If Mr. Slow used the strategy of guessing medians, then we should analyze his guesses if n is odd or even.\\
    Suppose n is even and $A=\{2k_{1},2k_{2},\cdots,2k_{n-1},2k_{n}\}$, then the position of $\hat{x}$ in A is  $$\{\underbrace{2k_{1},2k_{2},\cdots,2k_{\frac{n}{2}}}_{\frac{n}{2} \text{ elements}},\hat{x},\underbrace{2k_{\frac{n}{2}+1},\cdots,2k_{n-1},2k_{n}}_{\frac{n}{2} \text{ elements}}\}$$
    We can see that $\hat{x}$ is in the middle of the set and $\hat{x} \neq 2k_{\textit{i}}$ ($\textit{i} \in [1,n]$). Therefore, as proven in Q.4, if the real score $x_{real}$ lies to the right or left of $\hat{x}$, then $\hat{x}$ is guaranteed to be closer to $x_{real}$ than at least half of the guesses.\\
    On the other hand, if n is odd and $B=\{2l_{1},2l_{2},\cdots,2l_{n-1},2l_{n}\}$, then $\hat{x} = 2l_{\frac{n+1}{2}}$, i.e.
    $$\{2l_{1},2l_{2},\cdots,\underbrace{2l_{\frac{n+1}{2}}}_{\text{substituted by } \hat{x}},\cdots,2l_{n-1},2l_{n}\}$$
    This means that if Mr. Slow did not guess the real score on the dot, then he can only guess better than $\frac{n-1}{2}$ of his colleagues which is less than half, i.e. $\frac{n-1}{2} < \frac{n}{2}$.\\
    Hence, there is only a winning strategy when n is even.
    \item The answer should probably the same as part a, i.e. Mr. Slow will have a winning strategy for even number of colleagues but no guaranteed strategy for odd number of colleagues. One thing worth noting is that in the even case, Mr. Slow's guess will not always be an integer, it can be a fraction.
    \item No, it is not possible for Mr. Slow to formulate a winning strategy for him to be better than 60\% of his colleagues. It is because there is not enough information for him to make inference with the real score. The maximum he can do is just 50\% for the information provided.
    \item No, it is not possible as well. For Mr. Slow to make a faster guess, his margin of error will increase.
\end{enumerate}


\newpage
\item (Question 7: Textbook Question 1.32)
\begin{tcolorbox}[colback=blue!15]
Let T be a triangle with angles of 30, 60 and 90 degrees whose hypotenuse is of length 1. We choose ten points inside T at random. Prove that there will be four points among them that can be covered by a half-circle of radius 0.42.
\end{tcolorbox}
\textbf{Approach 1:} (Division of Angle)\\
Since we are randomly allocating the 10 points into T, the initial thought is to divide T into 10 equal regions such that each region should contain 1 point if the points are allocated evenly.
\begin{center}
\begin{tikzpicture}[
my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
\draw   (0,0) coordinate[label=below:$A$] (a) --
        (4,0) coordinate[label=below:$C$] (c) --
        (4,6.92820323) coordinate[label=above:$B$] (b) -- cycle;
\pic[my angle, "$\alpha=\SI{60}{\degree}$"] {angle = c--a--b};
\draw[red,thick,dashed] (4,6.92820323) -- (0.4,0)
                        (4,6.92820323) -- (0.8,0)
                        (4,6.92820323) -- (1.2,0)
                        (4,6.92820323) -- (1.6,0)
                        (4,6.92820323) -- (2,0)
                        (4,6.92820323) -- (2.4,0)
                        (4,6.92820323) -- (2.8,0)
                        (4,6.92820323) -- (3.2,0)
                        (4,6.92820323) -- (3.6,0);
\filldraw[blue] (0.25, 0.2) circle (2pt)
                (0.65, 0.2) circle (2pt)
                (1.05, 0.2) circle (2pt)
                (1.45, 0.2) circle (2pt)
                (1.85, 0.2) circle (2pt)
                (2.25, 0.2) circle (2pt)
                (2.65, 0.2) circle (2pt)
                (3.05, 0.2) circle (2pt)
                (3.45, 0.2) circle (2pt)
                (3.85, 0.2) circle (2pt);
    \end{tikzpicture}
\end{center}
Here, if we have a semicircle of radius 0.42 and its center lies on AC, then the semicircle should include at least 4 points.
\begin{center}
\begin{tikzpicture}[
my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
\draw   (0,0) coordinate[label=below:$A$] (a) --
        (4,0) coordinate[label=below:$C$] (c) --
        (4,6.92820323) coordinate[label=above:$B$] (b) -- cycle;
\pic[my angle, "$\alpha=\SI{60}{\degree}$"] {angle = c--a--b};
\draw[red,thick,dashed] (4,6.92820323) -- (0.4,0)
                        (4,6.92820323) -- (0.8,0)
                        (4,6.92820323) -- (1.2,0)
                        (4,6.92820323) -- (1.6,0)
                        (4,6.92820323) -- (2,0)
                        (4,6.92820323) -- (2.4,0)
                        (4,6.92820323) -- (2.8,0)
                        (4,6.92820323) -- (3.2,0)
                        (4,6.92820323) -- (3.6,0);
\filldraw[blue] (0.25, 0.2) circle (2pt)
                (0.65, 0.2) circle (2pt)
                (1.05, 0.2) circle (2pt)
                (1.45, 0.2) circle (2pt)
                (1.85, 0.2) circle (2pt)
                (2.25, 0.2) circle (2pt)
                (2.65, 0.2) circle (2pt)
                (3.05, 0.2) circle (2pt)
                (3.45, 0.2) circle (2pt)
                (3.85, 0.2) circle (2pt);
\draw[black,thick,dashed] (-1.36,0) -- (5.36,0) arc(0:180:3.36) -- cycle;
    \end{tikzpicture}
\end{center}
\textit{Remark}:\\
However, this method is incomplete. Since the points are randomly assigned, we cannot assume that they all lie evenly in each sub-triangle, i.e. we cannot assume the position of the pigeons.\\\\
\textbf{Approach 2:} (Semicircle Partition)\\
This approach is the most refined approach. Since we can fully cover the whole triangle T by 2 semicircles, we can arrange the points as follow:
\begin{center}
\begin{tikzpicture}[
my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
\draw   (0,0) coordinate[label=below:$A$] (a) --
        (4,0) coordinate[label=below:$C$] (c) --
        (4,6.92820323) coordinate[label=above:$B$] (b) -- cycle;
\pic[my angle, "$\alpha=\SI{60}{\degree}$"] {angle = c--a--b};
\draw[black,thick,dashed] (-1.36,0) -- (5.36,0) arc(0:180:3.36) -- cycle
                          (4,0.20820323) -- (4,6.92820323) arc(90:270:3.36) -- cycle;
\filldraw[blue] (0.5, 0.2) circle (2pt)
                (1, 1) circle (2pt)
                (1.2, 0.2) circle (2pt)
                (2.5, 3.8) circle (2pt)
                (3, 4.8) circle (2pt)
                (3.5, 4.3) circle (2pt);
    \end{tikzpicture}
\end{center}
Here, we can see that if 7 points are randomly assigned into T, then there are 2 cases where the the extra pigeon can lie in:
\begin{enumerate}
    \item The overlapping region
    \item One of the semicircles
\end{enumerate}
\begin{center}
\begin{tikzpicture}[
my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
\draw   (0,0) coordinate[label=below:$A$] (a) --
        (4,0) coordinate[label=below:$C$] (c) --
        (4,6.92820323) coordinate[label=above:$B$] (b) -- cycle;
\pic[my angle, "$\alpha=\SI{60}{\degree}$"] {angle = c--a--b};
\draw[black,thick,dashed] (-1.36,0) -- (5.36,0) arc(0:180:3.36) -- cycle
                          (4,0.20820323) -- (4,6.92820323) arc(90:270:3.36) -- cycle;
\filldraw[blue] (0.5, 0.2) circle (2pt)
                (1, 1) circle (2pt)
                (1.2, 0.2) circle (2pt)
                (2.5, 3.8) circle (2pt)
                (3, 4.8) circle (2pt)
                (3.5, 4.3) circle (2pt);
\filldraw[red] (2.5,2) circle (2pt);
    \end{tikzpicture}
\end{center}
\begin{center}
\begin{tikzpicture}[
my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
\draw   (0,0) coordinate[label=below:$A$] (a) --
        (4,0) coordinate[label=below:$C$] (c) --
        (4,6.92820323) coordinate[label=above:$B$] (b) -- cycle;
\pic[my angle, "$\alpha=\SI{60}{\degree}$"] {angle = c--a--b};
\draw[black,thick,dashed] (-1.36,0) -- (5.36,0) arc(0:180:3.36) -- cycle
                          (4,0.20820323) -- (4,6.92820323) arc(90:270:3.36) -- cycle;
\filldraw[blue] (0.5, 0.2) circle (2pt)
                (1, 1) circle (2pt)
                (1.2, 0.2) circle (2pt)
                (2.5, 3.8) circle (2pt)
                (3, 4.8) circle (2pt)
                (3.5, 4.3) circle (2pt);
\filldraw[red] (2.3,0.2) circle (2pt);
    \end{tikzpicture}
\end{center}
By the Pigeonhole Principle, a semicircle of radius 0.42 will cover at least 4 points.
\begin{flushright}
$\square$
\end{flushright}
\textit{Remark}:\\
The semicircle partition method is a typical pigeonhole method. However, we can see that we only need 7 points for this pigeonhole problem to work. Therefore, 10 points itself is definitely an overkill for this partition.\\

\item (Follow-up Question: Pyramid and Hemisphere)
\begin{tcolorbox}[colback=blue!15]
Now, instead of working on a 2-dimensional problem, we have the same problem but ascended to 3-dimensions. Let T be a right square pyramid with sides of 1. We place 5 points inside T, each has to be at least 1cm apart. Prove that there will be at least 1 point among them that can be covered by a hemisphere of radius 0.5.
\end{tcolorbox}
\textit{Proof}\\
Consider the otherwise that there exists 5 points inside T where distance of any 2 points $\ge 1$ and none of them can be covered by a hemisphere of radius 1. (denote the 5 points as A, B, C, D, E)\\
Since there are 4 non-overlapping regions between T and the hemisphere, for 4 of the points to be at least 1cm apart from each other, they have to locate at the 4 vertices of the base square of the pyramid.\\
Since there are 5 pigeons (A, B, C, D, E) and 4 pigeonholes (non-overlapping regions), by the Pigeonhole Principle, A has to be inside one of the non-overlapping regions as well, i.e. a non-overlapping region will contain at least 2 points. However, since the greatest distance between 2 points in a non-overlapping region $\leq 0.5$, contradiction!\\
Hence, A must be covered by the hemisphere.
\begin{flushright}
$\square$
\end{flushright}
\textit{Remark}:\\
The following is a graphical representation of how question 7 will work. It took me a lot of time to \LaTeX \, it up.
\begin{center}
\begin{tikzpicture}[scale=5,tdplot_main_coords]
%draw the main coordinate system axes
\draw[thick,->] (0,0,0) -- (1,0,0) node[anchor=north]{$x$};
\draw[thick,->] (0,0,0) -- (0,1,0) node[anchor=north west]{$y$};
\draw[thick,->] (0,0,0) -- (0,0,1.1) node[anchor=south]{$z$};

\tdplotsetthetaplanecoords{\phivec}
%draw some dashed arcs, demonstrating direct arc drawing
\draw[dashed,tdplot_rotated_coords] (\radius,0,0) arc (0:90:\radius);

\draw[dashed] (\radius,0,0) arc (0:360:\radius);
\shade[ball color=blue!15!white,opacity=0.2] (1cm,0) arc (0:-180:1cm and 5mm) arc (180:0:1cm and 1cm);

\draw[red,thick] (0,0,1) -- (1,-1,0) -- (1,1,0) -- (0,0,1) -- cycle
                 (0,0,1) -- (1,1,0) -- (-1,1,0) -- (0,0,1) -- cycle
                 (0.2,-1,0) -- (1,-1,0);
\draw[red,thick,dashed] (0,0,1) -- (-1,-1,0)
                        (-1,-1,0) -- (-1,1,0)
                        (-1,-1,0) -- (0.2,-1,0);
\shade[color=blue!50,opacity=0.2] (0,0,1) -- (1,-1,0) -- (1,1,0) -- (0,0,1) -- cycle
                                  (0,0,1) -- (1,1,0) -- (-1,1,0) -- (0,0,1) -- cycle
                                  (0,0,1) -- (-1,-1,0) -- (-1,1,0) -- (0,0,1) -- cycle
                                  (0,0,1) -- (1,-1,0) -- (-1,-1,0) -- (0,0,1) -- cycle;
\filldraw[blue] (1,1,0) circle (0.5pt) coordinate[label=below:$B$] (b)
                (1,-1,0) circle (0.5pt) coordinate[label=below:$C$] (c)
                (-1,-1,0) circle (0.5pt) coordinate[label=left:$E$] (e)
                (-1,1,0) circle (0.5pt) coordinate[label=right:$D$] (d)
                (0,0,1) circle (0.5pt) coordinate[label=right:$A$] (a);
\end{tikzpicture}
\end{center}


\newpage
\item (Question 9: Textbook Question 1.27)
\begin{tcolorbox}[colback=blue!15]
Find all 4-tuples (a,b,c,d) of distinct positive integers so that $a<b<c<d$ and 
$$\frac{1}{a}+\frac{1}{b}+\frac{1}{c}+\frac{1}{d}=1$$
\end{tcolorbox}
\textbf{Approach 1}: (Brute Force)\\
Given that $a,b,c,d \in \mathbb{N}$ and $a<b<c<d$. If $a=b=c=d$, then
$$\frac{1}{a}+\frac{1}{a}+\frac{1}{a}+\frac{1}{a}=1$$
$$\frac{4}{a}=1$$
$$a=4$$
This implies that $a<4$, i.e. $a \in \{1,2,3\}$. If $a=1$, then
$$\frac{1}{1}+\frac{1}{b}+\frac{1}{c}+\frac{1}{d}=1$$
$$\frac{1}{b}=\frac{1}{c}=\frac{1}{d}=0 \text{ (impossible!)}$$
If $a=3$, then the maximum number we can obtain is
$$\frac{1}{3}+\frac{1}{4}+\frac{1}{5}+\frac{1}{6}=\frac{19}{20}<1$$
Therefore, $a=2$ and we have 
$$\frac{1}{2}+\frac{1}{b}+\frac{1}{c}+\frac{1}{d}=1$$
$$\frac{1}{b}+\frac{1}{c}+\frac{1}{d}=\frac{1}{2}$$
Again, if $b=c=d$, then
$$\frac{1}{b}+\frac{1}{b}+\frac{1}{b}=\frac{1}{2}$$
$$\frac{3}{b}=\frac{1}{2}$$
$$b=6$$
Thus, the range of b is $3 \leq b < 6$, i.e. $b \in \{3,4,5\}$.
Here, we have to find the values of c and d by cases:
\begin{enumerate}
    \item If $b=3$
    $$\frac{1}{3}+\frac{1}{c}+\frac{1}{d}=\frac{1}{2}$$
    $$\frac{1}{c}+\frac{1}{d}=\frac{1}{6}$$
    Here, we can see that $6<c<12$, i.e. $c \in \{7,8,9,10,11\}$.
    Hence, when $a=2$ and $b=3$, by substitution, we can see that there are 4 sets of 4-tuples that satisfy the equality:
    $$\{2,3,7,42\},\{2,3,8,24\},\{2,3,9,18\},\{2,3,10,15\}$$
    \item If $b=4$
    $$\frac{1}{4}+\frac{1}{c}+\frac{1}{d}=\frac{1}{2}$$
    $$\frac{1}{c}+\frac{1}{d}=\frac{1}{4}$$
    Here, we can see that $4<c<8$, i.e. $c \in \{5,6,7\}$.
    Hence, when $a=2$ and $b=4$, by substitution, we can see that there are another 2 sets of 4-tuples that satisfy the equality:
    $$\{2,4,5,20\},\{2,4,6,12\}$$
    \item If $b=5$
    $$\frac{1}{5}+\frac{1}{c}+\frac{1}{d}=\frac{1}{2}$$
    $$\frac{1}{c}+\frac{1}{d}=\frac{3}{10}$$
    Here, we can see that $5<c<6.67$, i.e. $c=6$. Hence, if $a=2$, $b=5$, and $c=6$, we can see that d is
    $$\frac{1}{2}+\frac{1}{5}+\frac{1}{6}+\frac{1}{d}=1$$
    $$\frac{1}{d}=\frac{2}{15}$$
    $$d=7.5 \notin \mathbb{N}$$
    Therefore, there are no 4-tuples that satisfy the equality when $b=5$.
\end{enumerate}
Hence, there are 6 sets of 4-tuples that satisfy the equality, which are $$\{2,3,7,42\},\{2,3,8,24\},\{2,3,9,18\},\{2,3,10,15\},\{2,4,5,20\},\{2,4,6,12\}$$\\
\textit{Remark}:\\
This brute force method works but is inefficient. Is there a better way in finding all the combinations of 4-tuples?\\



\newpage
\item (Follow-up Question: The n-Fraction Problem)
\begin{tcolorbox}[colback=blue!15]
Now, instead of working on a 4-tuple, we are now working on an n-tuples ($a_{1},a_{2},a_{3},\ldots,a_{n}$) of distinct positive integers so that $a_{1}<a_{2}<a_{3}<\cdots<a_{n}$ and 
$$\frac{1}{a_{1}}+\frac{1}{a_{2}}+\frac{1}{a_{3}}+\cdots+\frac{1}{a_{n}}=1$$
Is there a conjecture in finding the number of n-tuples? If so, what is the number of 10-tuples if $n=10$?
\end{tcolorbox}
\textbf{Approach 1}: (Analysis by Brute Force)\\
Given that $a_{1},a_{2},a_{3},\ldots,a_{n} \in \mathbb{N}$ and $a_{1}<a_{2}<a_{3}<\cdots<a_{n}$. If $a_{1}=a_{2}=a_{3}=\cdots=a_{n}$, then
$$\underbrace{\frac{1}{a_{1}}+\frac{1}{a_{1}}+\frac{1}{a_{1}}+\cdots+\frac{1}{a_{1}}}_{\text{n times}}=1$$
$$\frac{n}{a_{1}}=1$$
$$a_{1}=n$$
This implies that $1<a_{1}<n$, i.e. $a_{1}\in\{2,3,4,\ldots,n-1\}$\\
Here, we can see that the amount of calculations explodes as we have to consider $n-2$ amount of cases for $a_{1}$, and if we choose $a_{1}=2$, then
$$\frac{1}{2}+\frac{1}{a_{2}}+\frac{1}{a_{3}}+\cdots+\frac{1}{a_{n}}=1$$
$$\frac{1}{a_{2}}+\frac{1}{a_{3}}+\cdots+\frac{1}{a_{n}}=\frac{1}{2}$$
If $a_{2}=a_{3}=\cdots=a_{n}$, then
$$\underbrace{\frac{1}{a_{2}}+\frac{1}{a_{2}}+\cdots+\frac{1}{a_{n}}}_{n-1 \text{ times}}=\frac{1}{2}$$
$$\frac{n-1}{a_{2}}=\frac{1}{2}$$
$$a_{2}=2n-2$$
Here, $2<a_{2}<2n-2$, i.e. $a_{2} \in \{3,4,5,\ldots,2n-3\}$. Then there are $2n-5$ numbers that we have to consider for $a_{2}$, and the number increases by k times ($k\in \mathbb{N}$) depending on what we choose k to be.\\
For example, if $a_{2}=k$ where $k \in \{3,4,5,\ldots,2n-3\}$, then
$$\frac{1}{k}+\frac{1}{a_{3}}+\cdots+\frac{1}{a_{n}}=\frac{1}{2}$$
$$\frac{1}{a_{3}}+\cdots+\frac{1}{a_{n}}=\frac{k-2}{2k}$$
Again, if $a_{3}=a_{4}=\cdots=a_{n}$, then
$$\underbrace{\frac{1}{a_{3}}+\cdots+\frac{1}{a_{3}}}_{n-2 \text{ times}}=\frac{k-2}{2k}$$
$$\frac{n-2}{a_{3}}=\frac{k-2}{2k}$$
$$a_{3}=\frac{2k(n-2)}{k-2}$$
Since the largest number $a_{3}$ can be is 3, then $a_{3}$ can at most be $6(n-2)-1$. Hence, there are $6(n-2)-4$ numbers we need to consider for $a_{3}$. The calculation can go on and on until we reach $a_{n}$ while each $a_{i}$ for $i \in \mathbb{N}$, we are considering more and more cases. Therefore, this brute-force method simply cannot work and a smarter and more elegant method has to be found in approaching this question.\\
This is an interesting problem as it relates deeply to the topic of Egyptian Fraction, i.e. every rational number can be represented by an Egyptian Fraction which is an expression with the numerator equals to 1 and the denominator equals to a positive integer.\\
The application of the above fraction and n-fraction problem can be a fascinating one. For example, if one wants to divide 1 pizza to 4 people, how many ways can we express such division?\\
The easiest way is indeed giving everyone $\frac{1}{4}$ of the pizza. However, since the denominators are required to be distinct

\end{enumerate}




\newpage
\section*{Topic 2: Inclusion-Exclusion Method}
\begin{enumerate}[\bf(1)]

\item (Question 1: Textbook Question 7.5)
\begin{tcolorbox}[colback=orange!15]
Let $p_1,\ldots,p_k$ be distinct prime numbers. Find a formula for $\Phi(p_1\cdots p_k)$.
\end{tcolorbox}
\textbf{Solution}:\\
Notice that for any $p_i$ where $i\in \mathbb{N}$, $\Phi(p_i)=p_i-1$. Therefore, we can immediately see that 
$$\Phi(p_1\cdots p_k)=(p_1-1)(p_2-1)\cdots(p_k-1)=\prod_{i=1}^k(p_i-1)$$



\item (Question 2: Textbook Question 7.6)
\begin{tcolorbox}[colback=orange!15]
Is it true that $\Phi(mn)=\Phi(n)\Phi(m)$, for all positive integers m and n?
\end{tcolorbox}
\textbf{Solution}:\\
Suppose m and n share a common prime factorization $\hat{P}_k$ for some $k \in \mathbb{N}$ such that
$$m=P_1^{a_1}\cdot P_2^{a_2}\cdots \hat{P}_k^{a_k}\cdots P_m^{a_m}$$
$$n=Q_1^{b_1}\cdot Q_2^{b_2}\cdots \hat{P}_k^{b_k}\cdots Q_n^{b_n}$$
where $P_i,Q_i \in$ Prime and $a_i,b_i \in \mathbb{N}$ ($i \in \mathbb{N}$).
By definition, we can see that 
$$\Phi(m)=m(1-\frac{1}{P_1})(1-\frac{1}{P_2})\cdots(1-\frac{1}{\hat{P}_k})\cdots(1-\frac{1}{P_m})$$
$$\Phi(n)=n(1-\frac{1}{Q_1})(1-\frac{1}{Q_2})\cdots(1-\frac{1}{\hat{P}_k})\cdots(1-\frac{1}{Q_n})$$
Whereas, since m and n share a common prime factor, then $\Phi(mn)$ now becomes
$$\Phi(mn)=mn(1-\frac{1}{P_1})(1-\frac{1}{P_2})\cdots(1-\frac{1}{P_m})\cdot(1-\frac{1}{\hat{P}_k})\cdot(1-\frac{1}{Q_1})(1-\frac{1}{Q_2})\cdots(1-\frac{1}{Q_n})$$
While, we can clearly see that $\Phi(m)\Phi(n)$ is
$$\Phi(m)\Phi(n)=\left[m(1-\frac{1}{P_1})(1-\frac{1}{P_2})\cdots(1-\frac{1}{\hat{P}_k})\cdots(1-\frac{1}{P_m})\right]\cdot\left[n(1-\frac{1}{Q_1})(1-\frac{1}{Q_2})\cdots(1-\frac{1}{\hat{P}_k})\cdots(1-\frac{1}{Q_n})\right]$$
$$=mn(1-\frac{1}{P_1})(1-\frac{1}{P_2})\cdots(1-\frac{1}{P_m})\cdot\left(1-\frac{1}{\hat{P}_k}\right)^2\cdot(1-\frac{1}{Q_1})(1-\frac{1}{Q_2})\cdots(1-\frac{1}{Q_n})$$
$$<mn(1-\frac{1}{P_1})(1-\frac{1}{P_2})\cdots(1-\frac{1}{P_m})\cdot(1-\frac{1}{\hat{P}_k})\cdot(1-\frac{1}{Q_1})(1-\frac{1}{Q_2})\cdots(1-\frac{1}{Q_n})=\Phi(mn)$$
Therefore, the statement is false
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
The solution given by the textbook is a simple counter-example of $\Phi(2)\Phi(4)<\Phi(8)$. Therefore, I have decided to rewrite the solution and produce a more general explanation why the statement is false for all positive integers m and n. However, one begs the question: will the statement be true if m and n are distinct primes instead?



\newpage
\item (Follow-up Question: Euler's Phi Function for Primes)
\begin{tcolorbox}[colback=orange!15]
Suppose now m and n are distinct primes, is it true that  $\Phi(mn)=\Phi(n)\Phi(m)$?
\end{tcolorbox}
\textbf{Solution}:\\
For $\Phi(mn)$, since m and n are distinct primes, then
$$\Phi(mn)=mn\left(1-\frac{1}{m}\right)\left(1-\frac{1}{n}\right)$$
$$=mn\left(1-\frac{1}{n}-\frac{1}{m}+\frac{1}{mn}\right)$$
$$=mn-m-n+1$$
$$=m(n-1)-(n-1)$$
$$=(m-1)(n-1)=\Phi(m)\Phi(n)$$
Therefore, the statement is true for all m, n where m and n are distinct primes
\begin{flushright}
$\square$
\end{flushright}






\end{enumerate}






\newpage
\section*{Topic 3: Enumeration}
\begin{enumerate}[\bf(1)]

\item (Question 1: Textbook Question 3.56)
\begin{tcolorbox}[colback=teal!15]
Let $P_{3}(r)$ be the number of $3\times3$ magic squares that are symmetric to their main diagonal. Prove that $P_{3}(r)\leq(r+1)^{3}$. 
\end{tcolorbox}

\item (Question 2: Textbook Question 3.57)
\begin{tcolorbox}[colback=teal!15]
How many $n\times n$ square matrices are there whose entries are 0 or 1 and in which each row and column has an even sum?
\end{tcolorbox}
\textbf{Approach 1}: (Odd and Even Counting Method)\\
The question is a bit complicated and we need to divide it into cases. Let's start with simpler cases, say when $n=4$,how many matrices are there that satisfies the above requirements? (Let's assume the matrices do not need to be in row-reduced echelon form and any rows 0 does not necessarily need to be at the bottom of the matrices)\\
My intuition is to choose the number of 1's (and 0's) on a row first, then choose the number of recurrence of the rows column-wise. Therefore, my counting method is to count a row from left to right first, then column from top to bottom.
$$
\begin{pmatrix}
\rn{11}{a_{11}}&\rn{12}{a_{12}}&\rn{13}{a_{13}}&\rn{14}{a_{14}}\\
\rn{21}{a_{21}}&\rn{22}{a_{22}}&\rn{23}{a_{23}}&\rn{24}{a_{24}}\\
\rn{31}{a_{31}}&\rn{32}{a_{32}}&\rn{33}{a_{33}}&\rn{34}{a_{34}}\\
\rn{41}{a_{41}}&\rn{42}{a_{42}}&\rn{43}{a_{43}}&\rn{44}{a_{44}}
\end{pmatrix}
$$
\begin{tikzpicture}[overlay, remember picture]
\draw[->, red](11)--(12)--(13)--(14);
\draw[->, blue](14)--(24)--(34)--(44);
\end{tikzpicture}
Let's start with a row. Since the sum of the row has to be even, then the number of individual entries (1's) we can choose on the row is also even (i.e. 0, 2, 4). So the number of combinations is $_{4}C_{0}$, $_{4}C_{2}$ and $_{4}C_{4}$ respectively.\\
In terms of columns, we can also choose an even number of rows that repeat the combination of 1's on the row above, i.e. $_{4}C_{0}$, $_{4}C_{2}$ and $_{4}C_{4}$.\\
For example, if we do $_{4}C_{2}$ on 1 row first, we simply need to choose the number of rows that repeats the above pattern, e.g. $_{4}C_{2}$. After that, we only need to fill the remaining spots with 0's and we will have a $4\times4$ matrix.
\begin{enumerate}
    \item Choose entries on a row (e.g. $_{4}C_{2}$)
    $$
    \begin{pmatrix}
    \boxed{\rn{11}{a_{11}}}&\rn{12}{a_{12}}&\boxed{\rn{13}{a_{13}}}&\rn{14}{a_{14}}\\
    \rn{21}{a_{21}}&\rn{22}{a_{22}}&\rn{23}{a_{23}}&\rn{24}{a_{24}}\\
    \rn{31}{a_{31}}&\rn{32}{a_{32}}&\rn{33}{a_{33}}&\rn{34}{a_{34}}\\
    \rn{41}{a_{41}}&\rn{42}{a_{42}}&\rn{43}{a_{43}}&\rn{44}{a_{44}}
    \end{pmatrix}
    \rightarrow
    \begin{pmatrix}
    \rn{11}{1}&\rn{12}{a_{12}}&\rn{13}{1}&\rn{14}{a_{14}}\\
    \rn{21}{a_{21}}&\rn{22}{a_{22}}&\rn{23}{a_{23}}&\rn{24}{a_{24}}\\
    \rn{31}{a_{31}}&\rn{32}{a_{32}}&\rn{33}{a_{33}}&\rn{34}{a_{34}}\\
    \rn{41}{a_{41}}&\rn{42}{a_{42}}&\rn{43}{a_{43}}&\rn{44}{a_{44}}
    \end{pmatrix}
    $$
    \item Choose number of repeating column-wise (e.g. $_{4}C_{2}$)
    $$
    \begin{pmatrix}
    \rn{11}{a_{11}}&\rn{12}{a_{12}}&\rn{13}{a_{13}}&\rn{14}{a_{14}}\\
    \rn{21}{a_{21}}&\rn{22}{a_{22}}&\rn{23}{a_{23}}&\rn{24}{a_{24}}\\
    \rn{31}{a_{31}}&\rn{32}{a_{32}}&\rn{33}{a_{33}}&\rn{34}{a_{34}}\\
    \rn{41}{a_{41}}&\rn{42}{a_{42}}&\rn{43}{a_{43}}&\rn{44}{a_{44}}
    \end{pmatrix}
    \rightarrow
    \begin{pmatrix}
    a_{11}&a_{12}&a_{13}&a_{14}\\
    1&a_{22}&1&a_{24}\\
    a_{31}&a_{32}&a_{33}&a_{34}\\
    1&a_{42}&1&a_{44}
    \end{pmatrix}
    $$
    \begin{tikzpicture}[overlay, remember picture]
    \draw[->, blue](21)--(22)--(23)--(24);
    \draw[->, blue](41)--(42)--(43)--(44);
    \end{tikzpicture}
    \item Fill the remaining entries with 0's
    $$
    \begin{pmatrix}
    0&0&0&0\\
    1&0&1&0\\
    0&0&0&0\\
    1&0&1&0
    \end{pmatrix}
    $$
\end{enumerate}
Here, we can start constructing a general formula from above. If we analyze from a row first. The general formula for choosing entries will be:
$$\sum_{k=0}^{\frac{n}{2}}{}_{n}C_{2k}=_{n}C_{0}+_{n}C_{2}+\cdots+_{n}C_{n}$$
For choosing the number of repeating rows column-wise, we have to consider 2 cases:
\begin{enumerate}
    \item $_{n}C_{0}$
    \item $_{n}C_{2}+\cdots+_{n}C_{n}$
\end{enumerate}
For (a), since we are choosing 0 entries from a row, there should not be any row with 1's, i.e. the matrix should be all 0's.\\
For (b), each combination from $_{n}C_{2}$ to $_{n}C_{n}$, there can be $_{n}C_{2}$ to $_{n}C_{n}$ number of repeating rows as well. Therefore, on modification, the general formula is:
$$(_{n}C_{0})^{2}+_{n}C_{2}\cdot\sum_{k=1}^{\frac{n}{2}}{}_{n}C_{2k}+_{n}C_{4}\cdot\sum_{k=1}^{\frac{n}{2}}{}_{n}C_{2k}+\cdots+_{n}C_{n}\cdot\sum_{k=1}^{\frac{n}{2}}{}_{n}C_{2k}=1+\sum_{j=1}^{\frac{n}{2}}{}(_{n}C_{2j}\cdot\sum_{k=1}^{\frac{n}{2}}{}_{n}C_{2k})$$
However, the above general formula does not work if n is odd. Therefore, with slight modification, the general formula for odd n is:
$$1+\sum_{j=1}^{\frac{n-1}{2}}{}(_{n}C_{2j}\cdot\sum_{k=1}^{\frac{n-1}{2}}{}_{n}C_{2k})$$
\textit{Remark}:\\
This method may seem plausible at first glance, yet it fails to consider arrangements like the following:
$$
\begin{pmatrix}
1&1&0&0\\1&1&0&0\\0&0&1&1\\0&0&1&1
\end{pmatrix}
$$
Since the method presented above counts the rows in repeating arrangements of entries, it actually under-counts certain number of cases in which the order of entries are different in some rows (yet they still add up to an even number row-wise and column-wise).\newpage

\textbf{Approach 2}: (Degree of Freedom)\\
Suppose we treat $n \times n$ square matrices of ascending sizes as appending a laterally-inverted "L" (indicated in \textit{red} below) on the lower-right of their corresponding $n-1 \times n-1$ matrices, then one argues that there is only 1 arrangement of 0's and 1's to fill out the "L", i.e. the degree of freedom of the "L" is 0 and it depends entirely on the 0-1 arrangement of its inner $n-1 \times n-1$ matrix.
$$
\begin{pmatrix}
\rn{11}{a_{11}}&\rn{12}{a_{12}}&\rn{13}{a_{13}}&\rn{14}{a_{14}}\\
\rn{21}{a_{21}}&\rn{22}{a_{22}}&\rn{23}{a_{23}}&\rn{24}{a_{24}}\\
\rn{31}{a_{31}}&\rn{32}{a_{32}}&\rn{33}{a_{33}}&\rn{34}{a_{34}}\\
\rn{41}{a_{41}}&\rn{42}{a_{42}}&\rn{43}{a_{43}}&\rn{44}{a_{44}}
\end{pmatrix}
$$
\begin{tikzpicture}[overlay, remember picture]
\draw[-, red](41)--(42)--(43)--(44);
\draw[-, red](14)--(24)--(34)--(44);
\end{tikzpicture}
In order to find out how the number of even-sum matrices changes with n, we can write out a few cases to help us visualize the pattern:\\
When $n=1$, there is only 1 way to fill out the matrix.
$$
\begin{pmatrix}
0
\end{pmatrix}
$$
When $n=2$, there are only 2 ways to fill out the inner $1 \times 1$ matrix, i.e. either 0 or 1.
$$
\begin{pmatrix}
0&\cdot\\\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&\cdot\\\cdot&\cdot
\end{pmatrix}
$$
When $n=3$, after listing out all the possibilities, there are 16 arrangements in its respective $2 \times 2$ inner matrix.
$$
\begin{pmatrix}
0&0&\cdot\\0&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&0&\cdot\\0&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&1&\cdot\\0&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&0&\cdot\\1&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&0&\cdot\\0&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&1&\cdot\\0&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&1&\cdot\\0&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&0&\cdot\\1&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
$$
$$
\begin{pmatrix}
1&0&\cdot\\1&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&0&\cdot\\0&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&1&\cdot\\1&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&1&\cdot\\1&0&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&1&\cdot\\0&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
0&1&\cdot\\1&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&0&\cdot\\1&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix},
\begin{pmatrix}
1&1&\cdot\\1&1&\cdot\\\cdot&\cdot&\cdot
\end{pmatrix}
$$
Here, we can start to see a pattern and thus one argues that:
\begin{enumerate}
    \item Uniqueness: $\exists!$ 1 combination for the laterally-inverted "L" (degree of freedom $=0$) such that $\forall n \times n$ matrices where $n \in \mathbb{N}$, $\forall a_{ij}$ where $1 \leq i,j \leq n$ and $a_{ij}=0,1$; the sum of rows and columns of the $n \times n$ matrix $=2k$, $k \in \mathbb{N}\cup\{0\}$
    \item Existence: $\forall n \in \mathbb{N}$, the number of combinations of even matrices $=2^{(n-1)^2}$
\end{enumerate}
The intuition behind the general formula $2^{(n-1)^2}$ is that since the degree of freedom for the outermost "L" layer is 0, then the number of combinations of even-sum $n \times n$ matrix depends on its $n-1 \times n-1$ matrix. Also, for each entry in the $n-1 \times n-1$ matrix, there are 2 choices: either 0 or 1, hence, one hypothesizes that the number of combinations for any $n \times n$ matrices is $2^{(n-1)^2}$. Therefore, the complete proof of this question is as follow:\\
\textit{Proof}\\\\
\begin{enumerate}
    \item Uniqueness:\\ 
    Denote an $n \times n$ matrix as $P_n$, its inner $n-1 \times n-1$ matrix as $P_{n-1}$ and the laterally-inverted "L" entries as L. Suppose $\exists L_1, L_2$ such that $P_n \equiv P_{n-1}\cup L_1 \equiv P_{n-1}\cup L_2$ and $\forall i,j \in \mathbb{N},$ $1 \leq i,j \leq n$, $\sum_{i=1}^n a_{i\bar{j}} = 2k$ and $\sum_{j=1}^n a_{\bar{i}j} = 2l$ for $k,l \in \mathbb{N}\cup \{0\}$. Since $P_n \equiv P_n$ and $P_{n-1} \equiv P_{n-1}$, then by definition, $L_1 = P_n\symbol{92}P_{n-1} = L_2$. (Proof by Contrapositive)
    \item Existence:\\
    When $n=1$, $f(1)=2^{(1-1)^2}=2^0=1$. Hence, the base case holds.\\
    Suppose $\exists k \in \mathbb{N}$, $f(k)=2^{(k-1)^2}$ holds by induction hypothesis. Then, for $f(k+1)=2^{(k+1-1)^2}=2^{k^2}$ holds.
\end{enumerate}
\begin{flushright}
$\square$
\end{flushright}


\item (Follow-up Question: RREF Condition)
\begin{tcolorbox}[colback=teal!15]
Now, the matrices are required to be in Reduced Row Echelon Form. How many $n\times n$ square matrices are there whose entries are 0 or 1 and in which each row and column has an even sum?
\end{tcolorbox}
For any $n \times n$ matrices, there should only be 1 possibility for an even-sum RREF matrix, which is the 0 matrix. The reason is that if 0 or 1 is allowed to be filled into the matrix, when 1 is in one of the entries $a_{i\bar{j}}$, then there must at least one other 1-entry in $a_{\hat{i}\bar{j}}$ where $1 \leq i < \hat{i} \leq n$, i.e. if there exists a 1-entry in a certain column, then there must be at least another 1-entry in that same column such that the sum of that column will become even. However, if this is the case, then after any $n \times n$ matrices are being row-reduced, there will only be one 1-entry in each column such that the sum of that column is odd. Hence, only the 0 matrix in any n satisfies the criteria of being an RREF and having even-sum rows and columns.
\begin{flushright}
$\square$
\end{flushright}

\item (Follow-up Question: Symmetry Condition)
\begin{tcolorbox}[colback=teal!15]
Now, instead of working on any $n \times n$ matrices, we work on $3 \times 3$ matrices. Prove that for any $3 \times 3$ even-sum matrices, we can always find an axis of symmetry in any orientation such that the matrix is symmetrical against it.
\end{tcolorbox}
\textit{Proof}: (By Brute Force)\\
The simplest method of proving this claim is to list out all the $3 \times 3$ even-sum matrices
$$
\begin{pmatrix}
0&0&0\\0&0&0\\0&0&0
\end{pmatrix},
\begin{pmatrix}
1&0&1\\0&0&0\\1&0&1
\end{pmatrix},
\begin{pmatrix}
0&1&1\\0&0&0\\0&1&1
\end{pmatrix},
\begin{pmatrix}
0&0&0\\1&0&1\\1&0&1
\end{pmatrix},
\begin{pmatrix}
0&0&0\\0&1&1\\0&1&1
\end{pmatrix},
\begin{pmatrix}
1&1&0\\0&0&0\\1&1&0
\end{pmatrix},
\begin{pmatrix}
0&1&1\\0&1&1\\0&0&0
\end{pmatrix},
\begin{pmatrix}
0&0&0\\1&1&0\\1&1&0
\end{pmatrix},
$$
$$
\begin{pmatrix}
1&0&1\\1&0&1\\0&0&0
\end{pmatrix},
\begin{pmatrix}
1&0&1\\0&1&1\\1&1&0
\end{pmatrix},
\begin{pmatrix}
0&1&1\\1&0&1\\1&1&0
\end{pmatrix},
\begin{pmatrix}
1&1&0\\1&0&1\\0&1&1
\end{pmatrix},
\begin{pmatrix}
1&1&0\\0&1&1\\1&0&1
\end{pmatrix},
\begin{pmatrix}
0&1&1\\1&1&0\\1&0&1
\end{pmatrix},
\begin{pmatrix}
1&0&1\\1&1&0\\0&1&1
\end{pmatrix},
\begin{pmatrix}
1&1&0\\1&1&0\\0&0&0
\end{pmatrix}
$$
Here, we can see that for all the 16 matrices, one can draw an axis of symmetry either vertically, horizontally, or along the diagonal. Hence, the claim is proved.
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
Proof by brute force is a crude way in solving this question. When the question ascends to an $n \times n$ matrix problem, listing out all the possibilities is no longer an option. Therefore, a better way in approaching this question is to discover the underlying pattern of how symmetry and even-sum row/column correlates.



\newpage
\item (Follow-up Question: The Rubik's Cube Problem)
\begin{tcolorbox}[colback=teal!15]
Now, instead of working an $n \times n$ matrix. A student draws out six $3 \times 3$ matrices:
$$
\begin{pmatrix}
1&1&1\\1&1&1\\1&1&1
\end{pmatrix} \times 1 \;\;\;
\begin{pmatrix}
0&0&0\\0&0&0\\0&0&0
\end{pmatrix} \times 5
$$
He decided to stick the matrices onto a cube to form a $3 \times 3$ Rubik's Cube. After scrambling the Rubik's Cube a bit, he found out that for every 1's, he can make the adjacent numbers a 0 (i.e. there is no 2 consecutive 1's at any position on the Rubik's Cube, including the corners joining 3 faces of the cube). How many combinations are there for such an arrangement? Moreover, what is the optimal number of moves for the student to obtain such a result? 
\end{tcolorbox}
\textbf{Approach 1}: (Breaking-down into Small Sub-Sections)\\
The optimal solution is 3 moves.\\
The method used is still brute-forcing and counting, but there is a rationale behind this trial-and-error method, it is that every move has to affect the maximal number of positions of 1's in the Rubik's cube. Therefore, the most logical first move is to move the middle row/column of 1's. Here, we have 4 choices, e.g. column $\rightarrow$ up, column $\rightarrow$ down, row $\rightarrow$ right, and row $\rightarrow$ left.\\
W.l.o.g. say we have chosen column $\rightarrow$ up as our first move. For the ease of notation, say we have chosen the face with all 1's as the face at front. Then, denote the respective moves as follow
\begin{enumerate}
    \item U: Rotate the top (up) face clockwise
    \item U': Rotate the top (up) face anti-clockwise
    \item D: Rotate the bottom (down) face clockwise
    \item D': Rotate the bottom (down) face anti-clockwise
    \item L: Rotate the left face clockwise
    \item L': Rotate the left face anti-clockwise
    \item R: Rotate the right face clockwise
    \item R': Rotate the right face anti-clockwise
    \item F: Rotate the front face clockwise
    \item F': Rotate the front face anti-clockwise
    \item B: Rotate the back face clockwise
    \item B': Rotate the back face anti-clockwise
    \item M: Rotate the vertical slice clockwise
    \item M': Rotate the vertical slice anti-clockwise
    \item E: Rotate the horizontal slice clockwise
    \item E': Rotate the horizontal slice anti-clockwise
    \item S: Rotate the top slice clockwise
    \item S': Rotate the top slice anti-clockwise
\end{enumerate}
Again, since we have chosen M' as our first move.
Then the following moves are E' and then S, i.e. the whole sequence is M'-E'-S.\\
To count the number of combinations of such arrangements, one only need to count the number of combinations of the sequences for one of the 4 starting moves, i.e. M, M', E, E'.\\
After the starting move (chosen as M'), to affect the maximal number of 1's, there are 2 ways to move, either E or E'. After that the degree of freedom for the remaining move is 0 as it can only move away from the 1's.\\
Therefore, there are only $4\times2\times1=8$ optimal combinations.
\begin{flushright}
$\square$
\end{flushright}


\end{enumerate}



\newpage
\section*{Topic 4: Partitions}
\begin{enumerate}[\bf(1)]

\item (Definition 4.1: Composition)
\begin{tcolorbox}[colback=purple!15]
A sequence $(a_1, a_2, \ldots, a_k)$ of integers fulfilling $a_i \geq 0$ for all $i$, and $\sum_{i=1}^k a_i=n$ is called a \textit{weak composition} of n. If, in addition, the $a_i$ are positive for all $i \in [k]$, then the sequence $(a_1, a_2, \ldots, a_k)$ is called a \textit{composition} of n.
\end{tcolorbox}

\item (Definition 4.2: Balls-in-Bins Formula)
\begin{tcolorbox}[colback=purple!15]
$\forall n, k > 0$, the number of weak compositions of n balls into k bins is
$$\binom{n+k-1}{k-1}=\binom{n+k-1}{n}$$
\end{tcolorbox}
\textit{Proof}\\
Here, we construct a combinatorial proof for the composition of n. W.l.o.g. suppose we try to place 15 balls into 5 boxes, \{A, B, C, D, E\}. 
\begin{center}
    \begin{tikzpicture}
        \filldraw[black] (-8,0) circle (2pt)
                         (-7,0) circle (2pt)
                         (-6,0) circle (2pt)
                         (-5,0) circle (2pt)
                         (-4,0) circle (2pt)
                         (-3,0) circle (2pt)
                         (-2,0) circle (2pt)
                         (-1,0) circle (2pt)
                         (-0,0) circle (2pt)
                         (1,0) circle (2pt)
                         (2,0) circle (2pt)
                         (3,0) circle (2pt)
                         (4,0) circle (2pt)
                         (5,0) circle (2pt)
                         (6,0) circle (2pt);
        \draw[black] (-5,-2) rectangle (-4,-1)
                     (-3,-2) rectangle (-2,-1)
                     (-1,-2) rectangle (0,-1)
                     (1,-2) rectangle (2,-1)
                     (3,-2) rectangle (4,-1);
        \node(A) at (-4.5,-1.5) {A};
        \node(B) at (-2.5,-1.5) {B};
        \node(C) at (-0.5,-1.5) {C};
        \node(D) at (1.5,-1.5) {D};
        \node(E) at (3.5,-1.5) {E};
    \end{tikzpicture}
\end{center}
Here, instead of considering how to place the balls directly into the box, we can abstract k boxes and imagine it as $k-1$ slits being arranged with the n number of balls together. Therefore, in this case, we would have a total of 4 slits and 15 balls to be arranged. Hence, if we consider the positions of the slits first, the total number of arrangements is choosing the position of 4 slits out of 19 spots, where the remaining 15 balls can be filled up automatically. Or vice versa, we can choose the position of the 15 balls among the 19 spaces and then fill up the remaining spots with the slits.
\begin{flushright}
$\square$
\end{flushright}

\newpage
\item (Question 3: Textbook Question 5.5)
\begin{tcolorbox}[colback=purple!15]
Let m and n be positive integers so that $m \geq n$. Prove that the Stirling numbers of the second kind satisfy the recurrence relation
$$S(m,n)=\sum_{i=1}^m S(m-i,n-1)n^{i-1}$$
\end{tcolorbox}
\textit{Proof}\\
For L.H.S., it is immediate that $S(m,n)$ refers to the partition of $[m]$ into n parts.\\
For R.H.S., the expression $S(m-i,n-1)$ refers to the partition of the set $[m-i]$ into $n-1$ parts. Notice that $i \in [1,m], i \in \mathbb{N}$, taking away i elements from $[m]$ and distributing the remaining $m-i$ elements into $n-1$ parts, means that there are still $i$ elements to be arranged into n parts. Notice that if $m-i < n-1$, then $S(m-i,n-1)=0$. Therefore, for $S(m-i,n-1) \geq 1$, $m-i \geq n-1$. This means that 
$$S(m-i,n-1) \begin{cases} >0,&\text{ if } m-i \geq n-1 \\
=0,&\text{ if } m-i < n-1\end{cases}$$
Then, the summation would mean
$$\sum_{i=1}^m S(m-i,n-1)=S(m-1,n-1)+S(m-2,n-1)+\cdots+S(m-m,n-1)$$
$$=S(m-1,n-1)+\cdots+S(m-k,n-1)+\underbrace{0+\cdots+0}_{k \text{ elements}} \text{ }(\text{where } \exists k \text{ s.t. } m-k = n-1)$$
$$=\sum_{i=1}^k S(m-i,n-1)$$
Since by definition, that after arranging the ${m-i}^{th}$ element, the ${m-i+1}^{th}$ element is automatically assigned into the $n^{th}$ part. Hence, the remaining $m-i+2$, $m-i+3$, $\dots$, $m-1$, $m$ elements are randomly assigned to the existing n parts, in which there is a total of $i-1$ elements and each with $\binom{n}{1}$ choices to be arranged. In other words, this refers to
$$\underbrace{\binom{n}{1}\binom{n}{1}\cdots\binom{n}{1}}_{i-1 \text{ elements}}=n^{i-1}$$
Therefore, the product of both the summation and $n^{i-1}$ is equivalent to $S(m,n)$
\begin{flushright}
$\square$
\end{flushright}
\textit{Remark}:\\
The reason I chose to rewrite this solution is that the original solution given by the textbook is very brief and concise in which some parts of the proof is not thoroughly explained, such as the part where $m-i < n-1$ would not affect the results, or how $n^{i-1}$ is obtained and why the power is $i-1$ instead of $i$. The rewritten proof above tends to fill up the gaps in the given solution.



\newpage
\item (Question 4: Counting Number of Surjections $f:[n]\rightarrow[k]$)
\begin{tcolorbox}[colback=purple!15]
Prove that the number of surjections of a function $f:[n]\rightarrow[k]$ is $k!\cdot S(n,k)$.
\end{tcolorbox}
\textit{Proof}\\
For the surjective function $f:[n]\rightarrow[k]$ to exist, this would imply that $|[n]|\geq|[k]|$. This is because by definition of surjectivity, for every element in $[k]$, there would exist at least one element in $[n]$ such that $f(n)=k$. If otherwise that $n<k$, then it is impossible for $f(n)=k_1$ and $f(n)=k_2$ where $k_1 \neq k_2$.\\
Then, this means that the number of surjections is simply assigning n distinguishable objects into k partitions, which can be denoted by $S(n,k)$.\\
Suppose w.l.o.g. that we are assigning $n=\{a,b,c,d,e\}$ into 3 partitions, i.e. $S(5,3)$, then one arrangement example can be
$$\{a,b\},\{c,d\},\{e\}$$
However, since surjections also consider the arrangement of the partitions, i.e.
$$\{a,b\},\{c,d\},\{e\} \neq \{c,d\},\{a,b\},\{e\}$$
Therefore, we need to multiply $3!$ such that we do not undercount. Hence, in general, the number of surjections is 
$$k!\cdot S(n,k)$$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
This solution is rewritten because I think more can be elaborated when proving the number of surjections is $k!\cdot S(n,k)$. Also, I think the textbook when proving these claims combinatorially can use a bit of an example for visualization.



\newpage
\item (Follow-up Question: Total Number of Funtions)
\begin{tcolorbox}[colback=purple!15]
As we proved in question 4 that the number of surjections for a function is $k!\cdot S(n,k)$, then what is the total number of surjective functions $f:[n]\rightarrow[k]$?
\end{tcolorbox}
\textbf{Approach 1}: (Enumerative Analysis)
\textit{Proof}\\
Notice immediately that for every element in $[n]$, there are k choices for 1 to be mapped to, k choices for 2 to be mapped to,$\ldots$, k choices for n to be mapped to. This would mean
$$\underbrace{\binom{k}{1}\cdots\binom{k}{1}}_{n \text{ elements}}=k^n$$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
However, we notice in Topic 8: Permutation Cycle, we have proven an identity that
$$\sum_{k=0}^nS(n,k)\cdot(x)_k=x^n$$
Is it possible that it has some relationship with counting the total number of surjective functions?\\\\

\textbf{Approach 2}: (Application of Corollary 5.10)\\
\textit{Proof}\\
Consider $f:[n=10] \rightarrow [k=5]$, suppose the image of f, i.e. $\{f(1),f(2),\ldots,f(10)\}=\{c,d,e\}$, then it means that this particular partition is $S(10,3)$. From Question 4, we know that there are $3!\cdot S(10,3)$ surjections for this function.\\
Here, we classify each surjective function (of 3-partition) $f:[10]\rightarrow\{a,b,c,d,e\}$ based on their images, i.e. \{a,c,d\}, \{b,c,d\}, \{a,b,c\}, etc. Here, we would notice that there are $\binom{5}{3}$ subsets for 3-partition, and each subset has $3!\cdot S(10,3)$ surjections.\\
Therefore, we can immediately see that the total number of surjective functions for 3-partition subsets are
$$3!\cdot S(10,3)\cdot\binom{5}{3}=\frac{5!}{2!}S(10,3)=(5)_3\cdot S(10,3)$$
Hence, by generalizing the case to i-partition where $0\leq i \leq n$, we can see that there are $(k)_i\cdot S(n,i)$ functions for i-partitions. So, the total number of functions will be the summation of all possible i-partitions
$$\sum_{i=0}^nS(n,i)\cdot (k)_i=k^n$$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
The difficulty of this question is to compute the falling factorial, other than that, it is pretty much straight-forward to prove this statement combinatorially. In Topic 8, this question will be proved again in a different method.







\end{enumerate}



\newpage
\section*{Topic 5: Generating Functions}
\begin{enumerate}[\bf(1)]

\item (Definition 5.1: Generating Functions)
\begin{tcolorbox}[colback=black!15]
Let $\{f_n\}_{n\geq0}$ be a sequence of real numbers. Then the formal power series $$F(x)=\sum_{n\geq0}f_nx^n$$ is called the \textit{ordinary generating function} of the sequence $\{f_n\}_{n\geq0}$.
\end{tcolorbox} 



\item (Definition 5.2: Products of Generating Functions)
\begin{tcolorbox}[colback=black!15]
Let $\{a_n\}_{n\geq0}$ and $\{b_n\}_{n\geq0}$ be two sequences, and let 
$$A(x)=\sum_{n\geq0}a_nx^n \text{, and } B(x)=\sum_{n\geq0}b_nx^n$$ be their respective generating functions. Define 
$$c_n=\sum_{i=0}^na_ib_{n-i}$$, and let
$$C(x)=\sum_{n\geq0}c_nx^n$$. Then
$$A(x)B(x)=C(x)$$
In other words, the coefficient of $x^n$ in $A(x)B(x)$ is $c_n=\sum_{i=0}^na_ib_{n-i}$
\end{tcolorbox}



\newpage
\item (Question 3: Textbook Exercise 8.25)
\begin{tcolorbox}[colback=black!15]
Find an explicit formula for $a_n$ if $a_0=1$ and $a_{n+1}=3a_n+2^n$ if $n\geq0$.
\end{tcolorbox}
\textbf{Solution}:\\
Let $\{a_n\}_{n\geq0}$ be the required sequence and $A(x)=\sum_{n\geq0}a_nx^n$. Multiply both sides of $a_{n+1}=3a_n+2^n$ by $x^{n+1}$ and sum over all $n\geq0$, here we would obtain the following equation
$$\sum_{n\geq0}a_{n+1}x^{n+1}=\sum_{n\geq0}3a_nx^{n+1}+\sum_{n\geq0}2^nx^{n+1}$$
For L.H.S., we can see that it is a generating function which starts enumerating at $a_1$ instead of $a_0$. Therefore, it is equivalent to $A(x)-a_0$.\\
For R.H.S., since we can factor out $3x$ from the first term, then it would become $3xA(x)$. For the second term, we can factor out an $x$ and group up $2^n$ and $x^n$ to become $(2x)^n$. Then, we can see that the term is a sum of geometric series, and thus can be rewritten into $\frac{x}{1-2x}$. Therefore, the equation now becomes
$$A(x)-a_0=3xA(x)+\frac{x}{1-2x}$$
Upon rearranging the terms to obtain an explicit function for $A(x)$, we can see
$$A(x)=\frac{a_0}{1-3x}+\frac{x}{(1-2x)(1-3x)}$$
Notice that for the first term, we can rewrite it as
$$\frac{a_0}{1-3x}=\frac{1}{1-3x}=\sum_{n\geq0}3^nx^n$$
And for the second term, we need to use the method of partial functions to find the coefficient of $a_n$. Denote constants A and B such that
$$\frac{A}{1-2x}+\frac{B}{1-3x}=\frac{x}{(1-2x)(1-3x)}$$
Here, after multiplying both sides with $(1-2x)(1-3x)$, we can see that
$A(1-3x)+B(1-2x)=x \Rightarrow (-3A-2B)x+(A+B)=x$
Therefore, we can construct a system of equations to solve for A and B individually
$$
\begin{cases}
-3A-2B=1\\A+B=0
\end{cases}
$$
Here, we can see that $A=-1$ and $B=1$. Therefore, we can also see that
$$\frac{x}{(1-2x)(1-3x)}=\frac{-1}{1-2x}+\frac{1}{1-3x}=-\sum_{n\geq0}2^nx^n+\sum_{n\geq0}3^nx^n=\sum_{n\geq0}(3^n-2^n)x^n$$
Hence, by combining the first and second term obtained, we can see that
$$a_n=2\cdot3^n-2^n$$



\newpage
\item (Question 3: Textbook Exercise 8.25)
\begin{tcolorbox}[colback=black!15]
Find an explicit formula for $a_n$ if $a_0=1$, $a_1=4$, and $a_{n+2}=8a_{n+1}-16a_n$ for $n\geq0$.
\end{tcolorbox}
\textbf{Solution}:\\
Let $\{a_n\}_{n\geq0}$ be the required sequence and $A(x)=\sum_{n\geq0}a_nx^n$. Multiply both sides of $a_{n+2}=8a_{n+1}-16a_n$ by $x^{n+2}$ and sum over all $n\geq0$, here we would obtain the following equation
$$\sum_{n\geq0}a_{n+2}x^{n+2}=\sum_{n\geq0}8a_{n+1}x^{n+2}-\sum_{n\geq0}16a_nx^{n+2}$$
For L.H.S., we can see that the function starts enumerating at $a_2$. Therefore, it is equivalent to $A(x)-a_1-a_0$.\\
For R.H.S., we can factor out $8x$ in the first term. Then we would notice that it is a generating function without $a_0$, thus it would become $8x(A(x)-a_0)$. For the second term, we can simply factor out $16x^2$, then it would become $16x^2A(x)$. Therefore, the equation now becomes
$$A(x)-a_1-a_0=8x(A(x)-a_0)-16x^2A(x)$$
After rearranging the terms, we can now see that
$$A(x)=\frac{(1-8x)a_0}{(1-4x)^2}+\frac{a_1}{(1-4x)^2}$$
Here, we can decompose the terms as follow
$$A(x)=\frac{(1-4x-4x)a_0}{(1-4x)^2}+\frac{a_1}{(1-4x)^2}$$
$$A(x)=\frac{a_0}{1-4x}-\frac{4xa_0}{(1-4x)^2}+\frac{a_1}{(1-4x)^2}$$
Given that $a_0=1$ and $a_1=4$, we can see that
$$A(x)=\frac{1}{1-4x}-\frac{4x}{(1-4x)^2}+\frac{4}{(1-4x)^2}$$
For the first term, it is immediate to notice that it can be rewritten as
$$\frac{1}{1-4x}=\sum_{n\geq0}4^nx^n$$
For the second term, one has to do a bit more algebraic manipulation before applying the partial fraction method. We can rewrite the term as
$$\frac{4x}{(1-4x)^2}=\left(\frac{2\sqrt{x}}{1-4x}\right)^2=\left[\frac{2\sqrt{x}}{(1+2\sqrt{x})(1-2\sqrt{x})}\right]^2$$
Now we can apply partial fraction method. Let A and B be the constants such that
$$\frac{A}{1+2\sqrt{x}}+\frac{B}{1-s\sqrt{x}}=\frac{2\sqrt{x}}{(1+2\sqrt{x})(1-2\sqrt{x})}$$
Then, we are able to obtain $A=-\frac{1}{2}$ and $B=\frac{1}{2}$. Therefore, we can now rewrite the second term as follow
$$\left[\frac{2\sqrt{x}}{(1+2\sqrt{x})(1-2\sqrt{x})}\right]^2=\left[\frac{1}{2}\sum_{n\geq0}2^nx^{\frac{n}{2}}-\frac{1}{2}\sum_{n\geq0}(-1)^n\cdot 2^nx^{\frac{n}{2}}\right]^2$$
After expanding the second term, we are able to obtain a clean closed form as follow
$$\frac{1}{2}\sum_{n\geq0}2^{2n}x^n-\frac{1}{4}\sum_{n\geq0}(-1)^n\cdot 2^{2n}x^n$$
Moving on to the third term, we will be using the same method as that used on the second term. Therefore, we can see that
$$\frac{4}{(1-4x)^2}=\left[\frac{2}{1-4x}\right]^2=\left[\frac{2}{(1+2\sqrt{x})(1-2\sqrt{x})}\right]^2$$
Again, we apply the partial fraction method. Let C and D be the constants such that
$$\frac{C}{1+2\sqrt{x}}+\frac{D}{1-2\sqrt{x}}=\frac{2}{(1+2\sqrt{x})(1-2\sqrt{x})}$$
Here, we are able to obtain $C=D=1$. Therefore, we can now rewrite the third term as follow
$$\left[\frac{2}{(1+2\sqrt{x})(1-2\sqrt{x})}\right]^2=\left[\sum_{n\geq0}(-1)^2\cdot 2^nx^{\frac{n}{2}}+\sum_{n\geq0}2^nx^{\frac{n}{2}}\right]^2$$
Again, after expanding the third term, we can obtain a clean closed form as follow
$$2\sum_{n\geq0}2^{2n}x^n+2\sum_{n\geq0}(-1)^n\cdot 2^{2n}x^n$$
Therefore, we can combine the first, second and third term to obtain $A(x)$ as follow
$$A(x)=\frac{1}{1-4x}-\frac{4x}{(1-4x)^2}+\frac{4}{(1-4x)^2}$$
$$=\sum_{n\geq0}4^nx^n-\left[\frac{1}{2}\sum_{n\geq0}2^{2n}x^n-\frac{1}{4}\sum_{n\geq0}(-1)^n\cdot 2^{2n}x^n\right]+\left[2\sum_{n\geq0}2^{2n}x^n+2\sum_{n\geq0}(-1)^n\cdot 2^{2n}x^n\right]$$
$$=\sum_{n\geq0}\left[5\cdot 2^{2n-1}+9(-1)^n\cdot 2^{2n-2}\right]x^n$$
Hence, we can see that
$$a_n=5\cdot 2^{2n-1}+9(-1)^n\cdot 2^{2n-2}$$
\textbf{Remark}\\
This question is very similar to the previous question. However, the difficult part is the manipulation of algebra in solving the $(1-4x)^2$ and realizing early that $1-8x$ can be decomposed into $1-4x-4x$. Although this is not a particularly hard proof, there are also certain parts while factoring and combining powers in the summation that requires a bit more understanding in how the power of summation works. Overall, this question has tested on my ability in solving complex algebraic equations. 






\end{enumerate}


\newpage
\section*{Topic 6: Graph Theory}
\begin{enumerate}[\bf(1)]

\item (Question 1: Textbook Question 9.2)
\begin{tcolorbox}[colback=yellow!15]
Is it true that if a graph has a closed Eulerian trail, then it has an even
number of edges?
\end{tcolorbox}
By definition, an Eulerian trail is a closed trail which uses up all the edges of the graph once. Denote the endpoints of the trail as $U_0$ and $U_k$, then a closed trail implies that $U_0 = U_k$. Then one can easily generate counter-examples in this case, one example is the odd cycle graphs, i.e. $C_n$ for $n=2k+1$, $k \in \mathbb{N}$. Since $|E(C_n)|=2m+1$ for $n \in \{3, 5, 7, 9, \cdots\}$ and $m=2k+1$, $k \in \mathbb{N}$; hence, the statement is false.
\begin{flushright}
$\square$
\end{flushright}


\item (Question 2: Textbook Question 9.3)
\begin{tcolorbox}[colback=yellow!15]
Let G be a simple graph on 10 vertices and 28 edges. Prove that G contains a cycle of length 4.
\end{tcolorbox}
\textit{proof}\\
Notice that
$$\sum_{v \in V(G)}d(v)=2|E(G)|=2 \times 28=56$$
Since there are 10 vertices, then the average degree on each vertex is
$$\frac{\sum_{v \in V(G)}d(v)}{|V(G)|}=\frac{56}{10}=5.6$$
Therefore, there must be at least 2 vertices with $d(v) \geq 6$. Denote the 2 vertices as $v_1$ and $v_2$. Here, we can immediately see that $v_1$ and $v_2$ are adjacent.\\
If $v_1$ and $v_2$ are adjacent, then both of them will have $d(v)=5$ after subtracting the edge between them. Since G is a simple graph and there are 8 remaining vertices, by the Pigeonhole Principle, there will be at least 2 vertices in $V(G)\symbol{92}\{v_1\,v_2\}$ adjacent to both $v_1$ and $v_2$, we can denote them as $v_3$ and $v_4$. Since w.l.o.g., the same argument can be applied to $v_3$ and $v_4$ in the first place if we take them as the loci in the first place, hence, a $C_4$ cycle can be formed, i.e. $v_1-v_2-v_3-v_4-v_1$.
\begin{flushright}
$\square$
\end{flushright}
\begin{center}
    \begin{tikzpicture} [my angle/.style = {draw, fill=teal!30,
                   angle radius=7mm, 
                   angle eccentricity=1.1, 
                   right, inner sep=1pt,
                   font=\footnotesize} 
                   ]
    \filldraw[black] (-1, 5) circle (2pt)
                     (0, 5) circle (2pt)
                     (-4, 0.2) circle (2pt)
                     (-3, 0.2) circle (2pt)
                     (-2, 0.2) circle (2pt)
                     (-1, 0.2) circle (2pt)
                     (0, 0.2) circle (2pt)
                     (1, 0.2) circle (2pt)
                     (2, 0.2) circle (2pt)
                     (3, 0.2) circle (2pt);
    \node(v1) at (-1, 5.5) {$v_1$};
    \node(v2) at (0, 5.5) {$v_2$};
    \node(v3) at (-4, -0.2) {$v_7$};
    \node(v4) at (-3, -0.2) {$v_6$};
    \node(v5) at (-2, -0.2) {$v_5$};
    \node(v6) at (-1, -0.2) {$v_4$};
    \node(v7) at (0, -0.2) {$v_3$};
    \node(v8) at (1, -0.2) {$v_8$};
    \node(v9) at (2, -0.2) {$v_9$};
    \node(v10) at (3, -0.2) {$v_{10}$};
    \draw[black] (-1, 5) -- (-4, 0.2)
                 (-1, 5) -- (-3, 0.2)
                 (-1, 5) -- (-2, 0.2)
                 (-1, 5) -- (-1, 0.2)
                 (-1, 5) -- (0, 0.2)
                 (0,5) -- (-1, 0.2)
                 (0, 5) -- (0, 0.2)
                 (0,5) -- (1, 0.2)
                 (0,5) -- (2, 0.2)
                 (0,5) -- (3, 0.2);
    \draw[red, thick, dashed] (-1, 5) -- (-1, 0.2) -- (0, 5) -- (0, 0.2) -- (-1, 5);
    \end{tikzpicture}
\end{center}



\newpage
\item (Question 3: Textbook Question 9.29)
\begin{tcolorbox}[colback=yellow!15]
Prove that if in a simple graph G, there is a trail or walk from vertex A to vertex B, then there is also a path from A to B.
\end{tcolorbox}
\textit{Proof}\\
By definition, a trail refers to an alternating sequence of vertices and edges, i.e. $$u_0,e_0,u_1,e_1,u_2,\ldots,u_{k-1},e_{k-1},u_k$$
where $e_i=(u_{i-1},u_i)$ and no $e_i$ is repeated in the sequence.
Since the existence of an A-B trail implies that A and B are connected by at least one sequence of edges, to prove that an A-B path exists, one has to show that for any i in [0,k], no vertices (i.e. $u_i$) repeats and $A \neq B$ (not a closed trail). Suppose for any cycle $C_n$, $n \in [0,k]$, which exists within the A-B trail where the endpoints on the trail is $u_i'$, i.e. then the vertex-edge sequence of the cycle would be
$$u_i',e_i',u_{i+1}',e_{i+1}',\ldots,u_{i+l}', e_{i+l}',u_i'$$
Since any cycle can always be appended or removed from a trail sequence, i.e. one can always bypass the $u_i'-u_i'$ cycle by moving on from $u_i'$ to $u_{i+1}$. Hence, one can always form an A-B path.
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}:\\
The gist of this question is to understand the difference between a trail/walk and a path. A trail is a sequence of edges and vertices where no edge is used twice, whereas a path is a sequence of edges and vertices where no vertex is used twice. A path is a stricter condition than a trail and hence the implication holds in this case. One also sees that connectedness is an important concept in proving this relationship. The existence of an A-B trail automatically implies that G is a connected simple graph, and thus for any u, v in V(G), there would always be a u-v path connecting them.



\item (Follow-up Question: Path and Eulerian Graphs)
\begin{tcolorbox}[colback=yellow!15]
Suppose G is an Eulerian graph, shown that for any $u,v \in V(G)$, there exists a u-v path in between them
\end{tcolorbox}
\textit{Proof}\\
Suppose the otherwise that G is Eulerian and $\exists u,v \in V(G)$, there is no u-v path. Then G is not connected. Contradiction!
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}:\\
A Eulerian graph is defined to be a graph containing a closed trail which uses up all the edges in the graph. i.e. $\forall e_i=(u_i,u_i+1)$ where $i=0,1,2,\ldots,k-1$
\begin{enumerate}
    \item $e_i$ is distinct (no repeated edges)
    \item $u_0=u_k$ (closed trail)
    \item $\forall e_i$, $i=0,1,2,\ldots,k-1$, G contains all the edges
\end{enumerate}
Therefore, we can see that there are 2 necessary conditions for Eulerian graphs
\begin{enumerate}
    \item Connectedness
    \item Even-degree vertices: $\forall v \in V(G)$, $d(v)=2k$, $k \in \mathbb{N}$
\end{enumerate}


\newpage
\item (Follow-up Question: Eulerian Graphs and Hamiltonian Graphs)
\begin{tcolorbox}[colback=yellow!15]
A student claims that G is an Eulerian Graph if and only if it is Hamiltonian. Is he/she correct? If so, prove the statement.
\end{tcolorbox}
\textit{Proof}\\
\begin{enumerate}
    \item Eulerian $\Rightarrow$ Hamiltonian\\
    For any Eulerian graphs, there exists a Eulerian trail such that all edges are used once. As proven above, Eulerian graphs can be broken down into cycle components. For example, w.l.o.g. consider $K_5$ as follow\\\\
    \begin{center}
    \begin{tikzpicture}
        \filldraw[black] (0,0) circle (2pt)
                         (-2,-1.453) circle (2pt)
                         (-1,-3.453) circle (2pt)
                         (1,-3.453) circle (2pt)
                         (2, -1.453) circle (2pt);
        \draw[black] (0,0)--(-2,-1.453)--(-1,-3.453)--(1,-3.453)--(2, -1.453)--(0,0)--cycle;
        \draw[black] (0,0)--(-1,-3.453)
                     (-2,-1.453)--(1,-3.453)
                     (-1,-3.453)--(2,-1.453)
                     (2, -1.453)--(-2,-1.453)
                     (1,-3.453)--(0,0);
        \node(A) at (0, 0.5) {A};
        \node(B) at (-2.5,-1.453) {B};
        \node(C) at (-1.3,-3.753) {C};
        \node(D) at (1.3,-3.753) {D};
        \node(E) at (2.5,-1.453) {E};
    \end{tikzpicture}
    \end{center}
    Suppose the Eulerian trial starts at A, the the trail will be 
    $$A,AB,B,BC,C,CD,D,DE,E,EA,A,AC,C,CE,E,EB,B,BD,D,DA,A$$
    Here, we can break the trail up into 2 cycle components with A as the breaking point, namely
    \begin{enumerate}
        \item $A,AB,B,BC,C,CD,D,DE,E,EA,A$
        \item $A,AC,C,CE,E,EB,B,BD,D,DA,A$
    \end{enumerate}
    Both i and ii are Hamiltonian cycles containing all the vertices of G. Hence, direction $\Rightarrow$ holds.\\

    \item Hamiltonian $\Rightarrow$ Eulerian\\
    Suppose using the example of $K_5$ again, but this time we take away 1 edge, w.l.o.g. CD for this case. i.e. new graph becomes $K_5\symbol{92}\{CD\}$ as follow
    \begin{center}
    \begin{tikzpicture}
        \filldraw[black] (0,0) circle (2pt)
                         (-2,-1.453) circle (2pt)
                         (-1,-3.453) circle (2pt)
                         (1,-3.453) circle (2pt)
                         (2, -1.453) circle (2pt);
        \draw[black] (0,0)--(-2,-1.453)--(-1,-3.453)--(0,0)--cycle
                     (0,0)--(1,-3.453)--(2, -1.453)--(0,0)--cycle;
        \draw[black] (0,0)--(-1,-3.453)
                     (-2,-1.453)--(1,-3.453)
                     (-1,-3.453)--(2,-1.453)
                     (2, -1.453)--(-2,-1.453)
                     (1,-3.453)--(0,0);
        \node(A) at (0, 0.5) {A};
        \node(B) at (-2.5,-1.453) {B};
        \node(C) at (-1.3,-3.753) {C};
        \node(D) at (1.3,-3.753) {D};
        \node(E) at (2.5,-1.453) {E};
    \end{tikzpicture}
    \end{center}
    One can still find a Hamiltonian cycle, which is $A,AC,C,CE,E,EB,B,BD,D,DA,A$. However, the graph is no longer Eulerian because $d(C)=d(D)=3$. Hence, the direction $\Leftarrow$ does not hold.\\
    In short, only Eulerian $\Rightarrow$ Hamiltonian holds.
\begin{flushright}
$\square$
\end{flushright}



\newpage
\item (Question 6: Textbook Question 9.49)
\begin{tcolorbox}[colback=yellow!15]
Let G be a simple graph on vertex set $[n]$ in which each vertex has degree two.
\begin{enumerate}
    \item Prove that G is a union of disjoint cycles.
    \item Let $g(n)$ be the number of graphs described above, and set $g(0)=1$. Prove that
    $$\sum_{n\geq0}g(n)\frac{x^n}{n!}=\frac{e^{-\frac{x}{2}-\frac{x^2}{4}}}{\sqrt{1-x}}$$
    \item Explain why the generating function computed in part (b) is different from the exponential generating function 
    $$\sum_{n\geq0}n!\frac{x^n}{n!}=\frac{1}{1-x}$$
    of the numbers of n-permutations, when permutations are in fact also unions of disjoint cycles on the set $[n]$.
\end{enumerate}
\end{tcolorbox}
\textbf{Part i)}:\\
\textit{Proof}\\
Suppose 


    

    
\end{enumerate}




\end{enumerate}


\newpage
\section*{Topic 7: Trees}

\begin{enumerate}[\bf(1)]
\item (Question 1: Textbook Question 10.39)
\begin{tcolorbox}[colback=orange!15]
Prove that a tree always has more leaves than vertices of degree at least three.
\end{tcolorbox}
\textit{Proof}\\
Denote T as the tree with vertices of degree at least 3. Let $P_k=x_1x_2\cdots x_k$ be the maximal path in T.\\
Suppose the otherwise that there exists some arrangement of T such that the number of leaves are less than or equal to that of the vertices of degree at least 3. One argues that from vertices $x_2$ to $x_{k-1}$, each of them has degree of at least 3. This is because for $i\in[3,k-2]$, each $x_i$ is adjacent to both $x_{i-1}$ and $x_{i+1}$ to create a path; and each $x_i$ will branch out to a unique path which is i) \textit{not maximal} and ii) \textit{contains at least 1 leaf}. Then in the subgraph $x_2x_3\cdots x_{k-1}$, it will have at least $k-2$ leaves\\
Here, we analyze each sub-claims and prove them by contradiction
\begin{enumerate}
    \item Suppose the otherwise that one of the branches (denote as $x_ix_{\hat{i}+1}\cdots x_{\hat{i}+\hat{k}}$ for some $x_i$ in $x_2x_3\cdots x_{k-1}$) is maximal, then $P_k=x_1x_2\cdots x_k$ is not maximal as we can construct a longer path $P_{\hat{k}}=x_1x_2\cdots x_{i-1}x_ix_{\hat{i}+1}\cdots x_{\hat{i}+\hat{k}}$. Hence, contradiction.
    \item Suppose the otherwise that one of the branches (denote as $x_ix_{\hat{i}+1}\cdots x_{\hat{i}+\hat{k}}$ for some $x_i$ in $x_2x_3\cdots x_{k-1}$) has less than 1 leaf. Then either there exists at least one other vertex $x_{\hat{i}+\hat{k}+1}$ (of degree 1) that is adjacent to $x_{\hat{i}+\hat{k}}$, which makes $x_{\hat{i}+\hat{k}+1}$ the leaf of that branch. Or if throughout the whole branch extending out from $x_i$ where no leaf exists, then $x_{\hat{i}+\hat{k}}$ must connect with some vertices $x_j$ in T which forms a cycle in T $\Rightarrow$ T is not a tree anymore. Contradiction.
\end{enumerate}
Hence, we have proven that in $x_2x_3\cdots x_{k-1}$, there must be at least $k-2$ leaves. Now we claim that both $x_1$ and $x_k$ in the maximal path of T are leaves. W.l.o.g., suppose the otherwise that $x_k$ is not a leaf, then
\begin{enumerate}
    \item There must exist at least one other vertex $x_{k+1}$ that is adjacent to $x_k$ which implies that $x_1-x_k$ path is not maximal. Contradiction.
    \item $x_k$ is connected back to some $x_j$ in T such that T is not a tree. Contradiction.
\end{enumerate}
Hence, we can see that both $x_1$ and $x_k$ must be leaves. This implies that in $x_1x_2\cdots x_k$, there must be at least $k+1$ leaves. Since there are only k vertices in the maximal path, then by $k+1>k$, the statement is proved.
\begin{flushright}
$\square$
\end{flushright}



\newpage
\item (Question 2: Textbook Question 10.42)
\begin{tcolorbox}[colback=orange!15]
Prove that if n is large enough, then the following statement is true. For all graphs G on n vertices, at least one of G and $\bar{G}$ contains a cycle. How large must n be for this to hold?
\end{tcolorbox}
\textit{Proof}\\
Notice that $G\cup\bar{G}\equiv K_n$ for any $n\in \mathbb{N}$.
\begin{enumerate}
    \item If $n=1$, then $K_1$ itself is not a cycle.
    \item If $n=2$, then $K_2$ itself is not a cycle.
    \item If $n=3$, for any decomposition the $K_3$, none of which can form a cycle.
    \item If $n=4$, one counter-example is as follow\\
    \begin{center}
        \begin{tikzpicture}
            \filldraw[black] (-2,0) circle (2pt)
                             (-2,-2) circle (2pt)
                             (0,-2) circle (2pt)
                             (0,0) circle (2pt)
                             (1,0) circle (2pt)
                             (1,-2) circle (2pt)
                             (3,-2) circle (2pt)
                             (3,0) circle (2pt);
            \draw[black] (-2,0)--(-2,-2)
                         (-2,-2)--(0,-2)
                         (0,-2)--(0,0)
                         (1,0)--(3,-2)
                         (3,0)--(1,-2)
                         (1,0)--(3,0);
            \node(G) at (-1,-2.5) {G};
            \node(G') at (2,-2.5) {$\bar{G}$};
                         
        \end{tikzpicture}   
    \end{center}
    \item If $n=5$, one notices that by rephrasing the question, it is asking about the maximum number of n such that $K_n$ can be decomposed into 2 unique maximal paths, $P_{n_1}$ and $P_{n_2}$. Below is a $K_5$ graph
    \begin{center}
    \begin{tikzpicture}
        \filldraw[black] (0,0) circle (2pt)
                         (-2,-1.453) circle (2pt)
                         (-1,-3.453) circle (2pt)
                         (1,-3.453) circle (2pt)
                         (2, -1.453) circle (2pt);
        \draw[black] (0,0)--(-2,-1.453)--(-1,-3.453)--(1,-3.453)--(2, -1.453)--(0,0)--cycle;
        \draw[black] (0,0)--(-1,-3.453)
                     (-2,-1.453)--(1,-3.453)
                     (-1,-3.453)--(2,-1.453)
                     (2, -1.453)--(-2,-1.453)
                     (1,-3.453)--(0,0);
        \node(A) at (0, 0.5) {A};
        \node(B) at (-2.5,-1.453) {B};
        \node(C) at (-1.3,-3.753) {C};
        \node(D) at (1.3,-3.753) {D};
        \node(E) at (2.5,-1.453) {E};
    \end{tikzpicture}
    \end{center}
    W.l.o.g., one chooses to start the path at A. There is a total of $4!$ ways to form the maximal path which is $P_4$. For any $P_4$ formed, i.e. for any arrangements of $A-V_2-V_3-V_4-V_5$, its complement must contain a cycle either formed by the inner "star" cycle or the outer "pentagon" cycle.   
\end{enumerate}
One can prove by mathematical induction that for $n\geq5$, there must exist a cycle in either $G$ or $\bar{G}$. Hence, the statement holds when $n\geq5$
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
One difficult part of this question is to notice that the union of $G$ and $\bar{G}$ is actually $K_n$ for some $n\in \mathbb{N}$. After that, the technical part is to prove it by induction.



\newpage
\section*{Topic 8: Permutation Cycles}
\begin{enumerate}[\bf(1)]

\item (Definition 6.1: Generating Function for $c(n,k)$)
\begin{tcolorbox}[colback=red!15]
Let n be a fixed positive integer. Prove that
$$\sum_{k=0}^nc(n,k)x^k=x(x+1)\cdots(x+n-1)$$
\end{tcolorbox}
\textit{Proof}\\
\begin{enumerate}
    \item Base Case: When $n=1$:\\
    $c(1,0)x^0+c(1,1)x^1=0+1\cdot x=x$
    \item Induction Step: Assume the identity holds for $2\leq n \leq n-1$, then by induction hypothesis
    $$x(x+1)\cdots(x+n-2)=\sum_{k=0}^{n-1}c(n-1,k)x^k$$
    Multiply both sides by $x+n-1$, then
    $$L.H.S.=x(x+1)\cdots(x+n-2)(x+n-1)$$
    For R.H.S., one has to prove the following
    $$\sum_{k=0}^nc(n,k)x^k=(x+n-1)\left(\sum_{k=0}^{n-1}(n-1,k)x^k\right)$$
    Here, we can decompose $x+n-1$ into $x$ and $n-1$, then multiply both components with the summation
    $$x\sum_{k=0}^{n-1}c(n-1,k)x^k+(n-1)\sum_{k=0}^{n-1}c(n-1,k)x^k$$
    $$=\sum_{k=0}^{n-1}c(n-1,k)x^{k+1}+\sum_{k=0}^{n-1}(n-1)\cdot c(n-1,k)x^k$$
    $$=\sum_{k=1}^{n}c(n-1,k-1)x^k+\sum_{k=0}^{n-1}(n-1)\cdot c(n-1,k)x^k$$
    Here, we can do some factorization to group up the summation terms. However, notice that the former summation terms enumerates from 1 to n, whereas the latter term enumerates from 0 to n-1. Therefore, we can only extract a summation term enumerating from 1 to n-1 and will be left with 2 extra terms as follow
    $$(n-1)\cdot c(n-1,0)x^0+\sum_{k=1}^{n-1}\left[c(n-1,k-1)+(n-1)c(n-1,k)\right]x^k+c(n-1,n-1)x^n$$
    For the first term, we can clearly see that it is equal to 0, thus can be rewritten as $c(n,0)$. For the second term, by the identity in theorem 6.12 in the textbook, we can see that $c(n,k)=c(n-1,k-1)+(n-1)\cdot c(n-1,k)$. For the third term, since it is equal to 1, it can also be rewritten as $c(n,n)$. Therefore, we can see the R.H.S. now becomes
    $$c(n,0)+\sum_{k=1}^{n-1}c(n,k)x^k+c(n,n)$$
    $$=\sum_{k=0}^nc(n,k)x^k$$    
\end{enumerate}
Hence, by mathematical induction, the identity holds.
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
I have decided to rewrite the proof provided by the textbook partly because I am not good at permutation cycle and partitions. Also, the proof provided by the textbook is too brief and concise, i.e. a lot has been left to the readers to decipher. Therefore, I have chosen to use mathematical induction to prove the identity holds. Another step that can be done is to explain combinatorially how L.H.S. equates R.H.S., but I feel like my next part I would like to focus more on explaining how the above identity relates to the Stirling Number of the First Kind with signs.\\
We learnt in class that $s(n,k)$ is called the Stirling numbers of the first kind, while $c(n,k)$ is called the unsigned Stirling numbers of the first kind. The identity given in class is $s(n,k)=(-1)^{n-k}c(n,k)$. The next follow-up question tends to investigate and prove this identity.\\\\
\textbf{Note}\\
The following question relates to both permutation cycle and partition, and aims to prove an identity in set partition (Corollary 5.10) with the method of permutation cycle.



\newpage
\item (Follow-up Question: $S(n,k)$ and $c(n,k)$)
\begin{tcolorbox}[colback=red!15]
Let n be a fixed positive integer. Prove that
$$x^n=\sum_{k=0}^nS(n,k)(x)_k$$
\end{tcolorbox}
\textit{Proof}\\
As we have shown from question 1 that $\sum_{k=0}^nc(n,k)x^k=x(x+1)(x+2)\cdots(x+n-1)$, we can start working from this identity.\\
Firstly, we can substitute $x \rightarrow -x$, then the identity will become
$$\sum_{k=0}^n c(n,k)(-x)^k=(-x)(-x+1)(-x+2)\cdots(-x+n-1)$$
$$\sum_{k=0}^n c(n,k)(-1)^kx^k=(-1)^n\cdot\left[x(x-1)(x-2)\cdots(x-n+1)\right]$$
Notice that $x(x-1)(x-2)\cdots(x-n+1)$ is a falling factorial with a power of n. Therefore, we can denote it as $(x)_n$. This implies that $R.H.S.=(-1)^n\cdot(x)_n$. Also, from the textbook, one notices that one can convert between $x^n$ and $(x)_n$ as follow (interchangeably)
$$x^n=\sum_{k=0}^nS(n,k)\cdot(x)_k \iff (x)_n=\sum_{k=0}^ns(n,k)\cdot x^k$$
Therefore, one can multiply both sides of the identity by $(-1)^n$ as follow
$$(-1)^n\left[\sum_{k=0}^n c(n,k)(-1)^kx^k\right]=(-1)^n\left\{(-1)^n\cdot\left[x(x-1)(x-2)\cdots(x-n+1)\right]\right\}$$
$$\sum_{k=0}^n c(n,k)(-1)^kx^k=(-1)^n\cdot\left[x(x-1)(x-2)\cdots(x-n+1)\right]$$
$$\sum_{k=0}^n c(n,k)(-1)^{n-k}x^k=(-1)^{2n}\cdot\left[x(x-1)(x-2)\cdots(x-n+1)\right]$$
$$\sum_{k=0}^n c(n,k)(-1)^{n-k}x^k=x(x-1)(x-2)\cdots(x-n+1)=(x)_n$$
Here, we can see that the Stirling number of the first kind $s(n,k)=(-1)^{n-k}\cdot c(n,k)$. Therefore, the identity is now
$$\sum_{k=0}^ns(n,k)x^k=(x)_n$$
By the interchangeability property, we can rewrite the identity as
$$\sum_{k=0}^nS(n,k)(x)_k=x^n$$
Hence, the statement is proved.
\begin{flushright}
$\square$
\end{flushright}
\textbf{Remarks}\\
Here, we are able to explain what the textbook failed to explain. However, this identity creates further questions: How does the interchangeability (duality) property works? Why can the falling factorial on L.H.S. can be interchanged with power term of x on R.H.S.? The following question tends to investigate the reason behind.






\end{enumerate}








\end{enumerate}


\newpage
\section*{Topic 9: Journal Prompts}

\begin{enumerate}[\bf(1)]

\item (Week 1: Mathematical Skills)\\
Mathy people I know include Pythagoras, Hypatia, Leonhard Euler, Carl 
Friedrich Gauss, etc. One thing in common with them is their fervent passion towards math and their ability to continuously think on a math problem. Such skills of being able to focus on thinking about math and relating ordinary numbers together to find hidden conjectures are ones that I admire and hope to acquire. For me, I am able to approach a mathematical problem from different perspectives and hopefully find an appropriate angle in generating a solution/proof. My strength in math is that I am good a visualizing mathematical objects graphically, which would help understand certain math problems/conjectures more easily. One weakness I have is that I would take a considerable amount of time in problems related to counting, such as cardinality and number theory. I enjoyed drawing graphs and geometry when it comes to various math topics, though I don't like to work on proving them. Hence, in MAT344, I hope I can work more on my weakness and topics that I dislike, namely counting and proofs.

\newpage
\item (Week 3: Setting Goals)\\
As mentioned in the introduction, I hoped I can develop an analytical mindset in Combinatorics and polish my skills in writing proofs. Hence, based on the 5 SMART goals, I have proposed the following steps in achieving my goals:
\begin{enumerate}
    \item Drafts and finalized solutions to problems from lectures and textbook (high-energy + high-importance)
    \item Mistakes made in approaching the questions (low-energy + high-importance)
    \item Concept points I learnt after correctly solving them (low-energy + high-importance)
    \item Personal reflection on weekly journals (low-energy + high-importance)
    \item Comprehensive questions of multiple fields of study (high-energy + low-importance)
    \item Personal reflection on in-course growth and achievements (low-energy + high-importance)
\end{enumerate}
Based on the "S" in SMART goals, "polishing my skills in writing proofs" is indeed a bit too broad. To narrow this down, I would modify it into "increase the accuracy and enhance the formatting of my proofs". Also, I can narrow down "develop an analytical mindset" into something like "try to produce at least 2 approaches in solving each question chosen".\\
Based on "M", I can modify and combine the first and second goals into something like "generate at least 2 accurate and different approaches to textbook questions chosen from each topic".
Base on "T", the goal is definitely time-based as results have to be produced and presented by the end of this course.

\newpage
\item (Week 5: Imposter Phenomenon and Self-evaluation)\\
After taking the Clance Imposter Phenomenon Test, I have scored a 64, which implies that I have relatively significant impostorism. Impostorism does to some degree affect me in MAT344. For example, I would worry if I am able to sustain the same amount of effort input into the portfolio and generate consistent quality solutions. There are also inner mental comparison between me and other students taking the course as a lot of Mathematics specialists and CS students are enrolled in MAT344. I would constantly worry if I am able to understand and utilize MAT344 knowledge effectively and efficiently.\\
The reason why I believe the MCS department has a high average score on Impostorism is that students who are enrolled in MCS programs are generally high-achievers. Competition and comparison between students, the competitive learning environment of utm in general, and the increasing difficulty of course content when one progresses through upper years more or less start to overwhelm students, slowly eroding away one's confidence and lowering our expectation towards our own ability and achievements.\\
After reading the article "Feel like a Fraud", one thing that resonates with me the most is "change my thinking". Combining what I have read with some of my own thoughts, I think one way to tackle impostorism is to focus on the gains from learning/knowledge, or the rewards on curiosity; rather than the gains from marks and rewards from comparison/competition. I can treat my courses as an opportunity to learn new knowledge and a platform to utilize previously-learnt skills to develop my own skillset as a mathematician. Not saying that grades are not important, but constantly thinking about them can deprive one of the rewards and satisfaction from curiosity which is not a sustainable way of learning. MAT344 to some extent provided me with a platform to develop my curiosity in Combinatorics. I am able to choose between course contents that I want to drill into and produce interesting results from it. It also helped me a lot in learning and refining my latex coding skills. However, since this course is still grade-related, and the portfolio essentially worths 100\% of the course grade, there would still be a considerable amount of study pressure.\\

\newpage
\item (Week 6: Reflecting)
\begin{enumerate}
    \item When do you usually reflect?\\
    I usually reflect on how much I understand a mathematical theorem and how well I am able to apply/tweak it into solving problems. I usually reflect in times after receiving a grade in assignments/tests in other math courses, and in MAT344, I usually reflect when I felt I have solved a problem (the problems usually come with no solution). Through revisiting my solution step by step, I would try to analyze my solution as if I am redoing the whole question again myself, just to see if I am able to come up with the same answer. More often or not, if I felt I have solved some questions, I would tend to skip a lot of steps which are used to come up with some partial solutions. This is some sort of heuristic that would possibly cause me in overlooking some mistakes, either it is just some careless arithmetic errors, or some logical/methodological mistakes.
    \item How far back do you look when you reflect?\\
    I would usually reflect starting from my understanding of some basic theorems because a lot of times when I am revisiting those theorems, I would be able to discover new perspective in interpreting and applying those theorems. After that, I would reflect on whether my steps are correct and whether the correct theorem/method is applied.
    \item Explain how the lion-thorn (in the video) can be interpreted as an analogy for self-reflection?\\
    I believe the lion-thorn can be interpreted as a problem/issue that can be triggered from time to time. Self-reflection is the action to locate where the thorn is and try to eradicate it by pulling it out.
    \item List some examples of when you reflected while problem solving, and when you reflected about your journey in MAT344.\\
    While working on problems, I noticed that I have certain strengths and weaknesses in different topics, for example I noticed I am better at topics like Pigeonhole Principle, Enumeration (includes binomial theorems, permutation cycles, inclusion-exclusion), generating functions and graphs; but I am not very good at partitions. Therefore, it would be easier for me to come up with follow-up questions/novel combinatorial objects/conjectures for the former topics than the latter one. Certain topics like the Stirling numbers and bell numbers are still right now difficult to grasp.
    \item In what ways will you include self-reflection in your journey in MAT344 going forward?\\
    For questions I have done which are worth noting, including both difficult problems form the textbook and the novel conjectures I have come up with, I will write a small paragraph under \textbf{Remarks} about the things I have taken away from this question. the tricky parts I have noticed while solving it, and improvements I have made from previous attempts/feedback, etc. Examples include the jellybean problem, even-sum matrix, graph theory question 2, generating functions question 2, etc.
\end{enumerate}

\newpage
\item (Week 7: How to solve it)
\begin{enumerate}
    \item In your own words, explain Polya's four main phases of solving problems.\\
    \begin{enumerate}
        \item Phase 1: Understand the problem\\
        Notice the problem/question at hand. Find the gist/key part(s) of the problem by drawing out graphs, breaking down the problem into smaller parts, rephrasing the problem, revisiting related theorems, etc.
        \item Phase 2: Devise a plan\\
        Choose the best method in approaching the problem, one which can simplify the problem but not complicating it. For example, in the conjecture I came up with the jellybean problem, I used the method of graphing, guess and check, make an orderly list, look for a pattern, solve by progressive cases, and be creative. There are also other problems I approached using most or some of the methods I listed above, such as the even-sum matrix problem, the generating function problem, etc. (explain in which step did I apply which method)
        \item Phase 3: Carry out the plan\\
        This is simply typing/writing out the whole solution and connecting all the bits and pieces of thoughts together by one complete piece of proof/solution.
        \item Phase 4: Review/extend:\\
        After solving a conjecture/problem, rethink the whole process once. Think about where was I stuck at, what was the thing that troubled me the most? Is it something that I overlooked? A theorem that I did not understand thoroughly? Or a place of the problem that requires a flick/tweak in concept (abstraction/creativity)?\\
        Also, one can ask follow-up questions that is built based on solved problems that investigate in areas that one thinks is worth drilling into. For example, if one is asking about the relationship between trees and Hamiltonian graphs, then one might think how it relates to Eulerian graphs, or how Eulerian graphs relate to Hamiltonian graphs, or even how things would look like if some restrictions are lifted/flipped/added.
    \end{enumerate}
\end{enumerate}

\newpage
\item (Week 8: Progress)\\
\begin{enumerate}
    \item What is a skill that you've developed so far in the course, and what's one skill you still want to develop?\\
    Skills that I have developed include: Latex, generalizing complex conjectures, visualizing through graphing, guess and check, making grounded assumptions, rephrasing questions to capture the key\\
    Skills that I still want to develop: approach a complex question analytically, systematically (breaking into sub-questions) $\Rightarrow$ helps simplify the question at hand
    \item How do you typically measure/assess your progress when learning math?\\
    \begin{enumerate}
        \item Work on textbook questions and see if I can solve them
        \item Work on the portfolio and see which section lacks content
        \item See if I am able to solve the same problem using different methods
    \end{enumerate}
    \item How does the measurement criteria of "quantity of problems solved" or "grades" a good/bad measurement of progress, or produce healthy/toxic behaviours?\\
    I think the benefits of the above measurements provide quantifiable evidence of the progress of a student. It allows them to trace their progress with minimal effort. However, because of that, one downside is that student after solving/resolving a problem (that is either difficult or have scored low mark on), they will move one immediately to the next problem/topic without stopping and thinking about what they have taken away from that problem and what more they should learn from the problem apart from scoring full credit on it. For example, the question may have touched a different realm of mathematical concepts that students can explore freely and make relations with the knowledge they have learnt (I believe a big part of learning is to make little bridges between knowledge points, like wormholes connecting different mathematical universes, and when we are challenged with similar or a totally different problem, we are able to move from one spot of math to the opposite side through these little tunnels we have built previously).
    \item What concrete skills related to definitions, theorems, conjectures, proof reading/writing, or the theory aspects of the course can you develop without solving problems?\\
    Through revisiting theorems and conjectures, I have learnt how to throw the theorem into different conditions and analyze how it works in different scenarios.
    \item What is the one thing you will do differently in the rest of the course? One new thing you will do?\\
    I will definitely include a greater proportion for reflection in my portfolio because I now realize that reflection is equally if not more important than problem-solving and theory-crafting, because consolidating knowledge and locating the lion-thorn allows me to walk further in the path as a mathematician.
\end{enumerate}



\newpage
\item (Week 10: Creating Your Own Portfolio)
\begin{enumerate}
    \item L01: Demonstrate Expertise in the Following Topics
    \item L02: Analyze Novel Combinatorial Objects
    \item L03: Create Solutions to Problems, and Proofs of Theorems, Independently without the Help of Outside Resources, that are Coherent, Organized and Well-supported
    \item L04: Go Beyond Previously Solved Problems, and ask nnovel and interesting questions about those problems, that require new insights to solve\\
    I did partner with Kevin Ng in the course in solving a couple of textbook problems together. He found my Jellybean Conjecture quite impressive, especially when I was able to generalize the formula from the lattice path/pascal triangle instead of using generating functions.\\
    My signiture questions include: Jellybean Conjecture, n-fractions problem, even-sum matrices, Counting total number of surjective functions, and Generating Function for c(n,k)
    \item L05: Create and implement a personalized self-improvemnt plan by identifying strengths and weaknesses you have as a mathematician, and iterventions to improve them
    \begin{enumerate}
        \item How have I grown as a mathematician?
        \item Did I have to course correct at any point this term? i.e. I tried learning in a certain way, but later in the term I realized it wasn't working, so I did something different.
        No, not really. I was on a nice track.
        \item What important skills have I learnt about how I learn and create mathematics?\\
        Since my strength in mathematics is I am able to withstand boredom of listing out all the combinatorial objects rigorously, such ability allows me through trial and error generate new combinatorial objects and proofs, and discover hidden relationships/conjectures through repeatedly listing out objects. Because I am constantly challenged with new theorems and difficult problems, either in class, from the textbook, or those I created myself, I am forced to approach questions in multiple perspectives in attempt to understand and solving them. More often or not, such as in the even-sum matrix problem, jellybean conjecture, Stirling number problem, etc. I am able to find more than one way/explanation to the question in which each of them span across different topics taught.
        \item Have I applied any of my new skills in other courses or other parts of my life?\\
        Absolutely. In assignments from other courses/during exams, whenever I am stuck, I will recall what I have learnt, all the concepts, theorems, definitions, and I would list them out in my head and try to build a connection with the problem at hand. The bridge may be long and spans across multiple topics, but this is the part and process of learning, the integration of knowledge, although we classify knowledge into different categories, the ultimate goal is to use them whenever needed, and more often or not, problems in real life are not categorized and thus require knowledge and skills acquired from different fields to tackle.
        \item What is my biggest sucess in this course?\\
        Jellybean Problem. I found multiple ways in solving this question. And possibly a new combinatorial identity/Understand Partitions, especially Stirling numbers and Bell numbers.
        \item If I could take this course again, what would I do differently?\\
        Probably start doing the portfolio as early as possible and submit my solutions every week. Though it is a tough commitment. I'll probably take this course after I have taken MAT202 as well, I think it would make my life in understanding MAT344 concepts much more easier.
    \end{enumerate}
\end{enumerate}


\end{enumerate}


\end{document}
