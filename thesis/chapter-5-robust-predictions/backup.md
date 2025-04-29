%%%%%
%%
%% Sample document ``thesis.tex''
%%
%% Version: v0.2
%% Authors: Jean Martina, Rok Strnisa, Matej Urbas
%% Date: 30/07/2008
%%
%% Copyright (c) 2008-2011, Rok Strniša, Jean Martina, Matej Urbas
%% License: Simplified BSD License
%% License file: ./License
%% Original License URL: http://www.freebsd.org/copyright/freebsd-license.html
%%%%%

% Available documentclass options:
%
%   <all `report` document class options, e.g.: `a5paper`>
%   withindex   - enables the index. New index entries can be added through `\index{our entry}`
%   glossary    - enables the glossary.
%   techreport  - typesets the thesis in the technical report format.
%   firstyr     - formats the document as a first-year report.
%   times       - uses the `Times` font.
%   backrefs    - add back references in the Bibliography section
%
% For more info see `README.md`
% \documentclass[times]{cam-thesis}
\documentclass[a4paper,12pt,twoside,openright]{report}

% Citations using numbers
% \usepackage[numbers]{natbib}

\usepackage{xcolor}
\usepackage{caption}
\usepackage{subcaption}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{sectsty}
\usepackage{booktabs}
\usepackage{hyperref}
\usepackage{caption}
\usepackage{subcaption}
\usepackage{graphicx}

% \usepackage[showframe]{geometry}


% \usepackage[T1]{fontenc}
% \usepackage{crimson}
% \usepackage{fbb}
% \usepackage{charter}
% \usepackage{imfellEnglish}
% \usepackage{euscript}
\usepackage{biolinum}
% \usepackage{helvet}
% \usepackage{tgpagella}
% \usepackage{fbb}
\usepackage{tgpagella}
% \usepackage{times}

% \usepackage{libertine}
% \usepackage{libertinust1math}

% \renewcommand{\sfdefault}{ppl}

%\setlength{\parindent}{0em}
%\setlength{\parskip}{1em}

\newcommand{\ind}{\perp\!\!\!\!\perp} 

\usepackage{hyperref}
\usepackage{url}

% Recommended, but optional, packages for figures and better typesetting:
\usepackage{microtype}
\usepackage{graphicx}
% \usepackage{subfigure}
\usepackage{booktabs} % for professional tables

% For theorems and such
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{mathtools}
\usepackage{amsthm}

% if you use cleveref..
\usepackage[capitalize,noabbrev]{cleveref}

\usepackage{caption}
\usepackage{subcaption}
\usepackage{tabularx}
\newcolumntype{Y}{>{\centering\arraybackslash}X}

\newcommand{\fix}{\marginpar{FIX}}
\newcommand{\new}{\marginpar{NEW}}
% \newcommand{\change}[1]{\textcolor{blue}{#1}}
\newcommand{\draft}[1]{\textcolor{blue}{#1}}
\newcommand{\crit}[1]{\textcolor{red}{#1}}
\newcommand{\myparagraf}[1]{\textbf{#1}}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Thesis meta-information
%%

%% The title of the thesis:
\title{\bf Style-content disentanglement}

%% The full name of the author (e.g.: James Smith):
\author{Dan Andrei Iliescu}

%% College affiliation:
% \college{St Edmund's College}

%% College shield [optional]:
% \collegeshield{CollegeShields/Christs}
% \collegeshield{CollegeShields/Churchill}
% \collegeshield{CollegeShields/Clare}
% \collegeshield{CollegeShields/ClareHall}
% \collegeshield{CollegeShields/CorpusChristi}
% \collegeshield{CollegeShields/Darwin}
% \collegeshield{CollegeShields/Downing}
% \collegeshield{CollegeShields/Emmanuel}
% \collegeshield{CollegeShields/Fitzwilliam}
% \collegeshield{CollegeShields/Girton}
% \collegeshield{CollegeShields/GonCaius}
% \collegeshield{CollegeShields/Homerton}
% \collegeshield{CollegeShields/HughesHall}
% \collegeshield{CollegeShields/Jesus}
% \collegeshield{CollegeShields/Kings}
% \collegeshield{CollegeShields/LucyCavendish}
% \collegeshield{CollegeShields/Magdalene}
% \collegeshield{CollegeShields/MurrayEdwards}
% \collegeshield{CollegeShields/Newnham}
% \collegeshield{CollegeShields/Pembroke}
% \collegeshield{CollegeShields/Peterhouse}
% \collegeshield{CollegeShields/Queens}
% \collegeshield{CollegeShields/Robinson}
% \collegeshield{CollegeShields/Selwyn}
% \collegeshield{CollegeShields/SidneySussex}
% \collegeshield{CollegeShields/StCatharines}
% \collegeshield{CollegeShields/StEdmunds}
% \collegeshield{CollegeShields/StJohns}
% \collegeshield{CollegeShields/Trinity}
% \collegeshield{CollegeShields/TrinityHall}
% \collegeshield{CollegeShields/Wolfson}
% \collegeshield{CollegeShields/FitzwilliamRed}

%% Submission date [optional]:
% \submissiondate{June, 2023}

%% You can redefine the submission notice [optional]:
% \submissionnotice{A badass thesis submitted on time for the Degree of PhD}

%% Declaration date:
\date{March, 2024}
\title{Causally-robust predictions}

%% PDF meta-info:
% \subjectline{Computer Science}
% \keywords{one two three}

\newcommand{\flag}[1]{\textcolor[rgb]{0.9,0.3,0.3}{\textbf{#1}}}



%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Contents:
%%
\begin{document}

\allsectionsfont{\sffamily}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Title page, abstract, declaration etc.:
%% -    the title page (is automatically omitted in the technical report mode).
% \frontmatter{}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Thesis body:
%%
\chapter*{Robust predictions}

% \draft{\paragraph{Summary.} This section deals with the problem of supervised learning from interventional data. The setup is that we have multiple groups of data. Each group comprises of multiple samples. Each sample is a tuple $X, Y, U$ where $X$ is the observation, $Y$ is the target variable and $U$ is the confounder. The goal is to predict $Y$ from $X$, as in supervised learning. But the relationship between $X$ and $Y$ is confounded by $U$. However, the structure of the dataset offers us a help. Across groups, the variable $X$ has been intervened upon, such that each group comprises samples of data with a different intervention on $X$. I want to illustrate how the Group-Instance model that I introduce in my thesis can help with achieving more accurate causal predictions. The Group-Instance model is an autoencoder model that can encode a group of $K$ observations into one group-level representation and $K$ instance-level representations. How can we use the group structure to help us improve the accuracy of predictions? Well, it all has to do with the relationship between $U$ and the group. The distribution of confounder $U$ can vary across groups. The strength of this variation sits on a scale from 0 (i.e. the confounder is independent of the group) to total (all cases within a group have the same value for the confounder, and this value is different across groups). In middling cases on this scale, group-level latent variables don't have much to offer. But in the extreme cases, they do. SO there are 2 extreme cases. The first is when the group is independent of the confounder (i.e. the confounder variable $U$ has the same distribution across every group). The second is when the confounder variable is the same as the group (i.e. the value of the confounder variable is constant within the group and varies across groups). For the first case, we can use the group-level latent variable learned by the Group-Instance model as a synthetic instrumental variable to perform causal inference. This means training the Group-Instance model on the groups of observations and then using the group-level latent variable to predict both the observation and the outcome (using 2 different linear predictors). Then, by dividing the parameter of the outcome predictor by the parameter of the observation predictor, we obtain the causal parameter mapping the observation to the outcome. We claim that this group-level latent variable is a decent instrumental variable. We validate this claim by creating a toy dataset using known formulas and then showing that the parameter estimate obtained using our instrumental variable is better than the parameter estimate using simple maximum likelihood, and also than the parameter estimate using some popular but naive instrumental variables, like neighbour instrument. Now let's look at the second case. The solution there is to train a more accurate predictor by feeding the group-level latent variable as input. So this means that we train the Group-Instance model and use the output group variables as extra inputs when training the supervised predictor. This means concatenating the observation with the group-level latent variable and using that to predict the outcome. At test-time, we must receive a whole group of data, that we feed into the Group-Instance model to produce a group-level latent variable. This we concatenate with the observation and feed as input to the predictor. We claim that this predictor is better even than the true causal parameter. We show this empirically using another toy dataset.}

- The real strength of the argument comes from the algebra
  - Computer inversion of the gaussian versus real experiment
- Catastrophic forgetting is sometimes desirable when the features are not causal.
  - Simple maths example is useful for both.
- If you have a group, you can do better than the causal.
  - In a world with complete disentanglement, a single sample tells me what z is. 
- Degree of entanglement tells us if we need a group.
  - Fixed conditional shift, different group size lead to different disentanglement in the learned model.
- Group instance modelling is a wonderful thing to do to gain insight into a whole load of problems
  -  This is achievable IV, Peters
-  Spend 1 or 2 days writing this out


This chapter explains how our group-instance model can be used to improve predictions in the task of \textit{unsupervised domain adaptation}. This is the task of training a predictor to map one random variable onto another in such a way that can achieve high accuracy across multiple different environments, which are actually different joint distributions over those variables. I want to advance the conversation of the domain adaptation community from the current gold-standard of \textit{invariant predictors} (i.e., predictor functions that achieve the same accuracy across environments) to a new paradigm, which I call \textit{contextual predictors} (i.e., predictor functions that adapt their predictions to the current environment).

Concretely, we train a predictor function map an outcome variable $Y$ conditioned on an observation variable $X$. The training dataset comprises observation-outcome pairs sampled from $X, Y$.

In this chapter, I want to advance the conversation of the community about the problem of domain adaptation. I want to propose a new approach for overcoming the problem of poor generalisation in prediction models. I want to go past invariance and onto contextualisation. 

In domain adaptation, there are three kinds of shifts that happen between groups: covariate, conditional and target.

Learning a representation of the group can lead to all sorts of advantages.

The conventional approach for unsupervised domain adaptation is to learn a representation that is invariant to the change in environments.

Group-instance can leverage new information that wasn't previously available.
Conventional methods for domain adaptation use the group as a constraint. I use the group as another feature.

I think what I want to communicate in this chapter is:

\begin{enumerate}
    \item Sometimes the invariant (causal) predictor is not the best predictor. If the data you receive at test-time belongs to the same group, you can use the group information to make better predictions.
    \item Autoencoding groups (using the GID model) is a way to bring causal inference solutions (instrumental variables, controlling for confounders) to discrete domain problems.
    \item The way to make use of the group information depends on the nature of the groups. For example, if the groups represent different interventions on the confounder, then we can control for the effect of the confounder by using the group variable as a proxy. Conversely, if the groups are independent of the confounder, then we can use the group variable as an instrument to perform causal inference.
\end{enumerate}

\section{Introduction}

% This chapter illustrates the ability of the \textit{Group-Instance Disentanglement} model (\texttt{GID}) to achieve causally-robust predictions.

% We consider the problem of \textit{supervised learning} from \textit{interventional data} with \textit{confounding}. Supervised learning is the task of training a predictor function that achieves accurate predictions of an outcome variable $Y$ conditioned on an observation variable $X$. The training dataset comprises observation-outcome pairs sampled from $X, Y$. Confounding occurs when an unseen variable $U$ is a causal parent of both the observation $X$ and the target $Y$. Interventional data refers to a training set where the the observation-outcome pairs are assigned to different groups based on interventions on the observation $X$ and/or the confounder $U$.

\paragraph{Problem statement.} The training dataset comprises $N$ groups, each with a different number of observation-outcome pairs. Let $x_{i, k} \in \mathbb{R}$ be the $k$-th observation in group $i$, with $i \in \{1:N\}$ and $k \in \{1:K_i\}$. Let $y_{i,k}$ be the $k$-th outcome in group $i$. 

We assume that the data belonging to group $i$, the pairs $\{(x_{i,k}, y_{i,k})\}_{k=1}^{K_i}$, were generated by repeatedly sampling the joint distribution of the random variables $X_i, Y_i$. Let $U_i$ be the unobserved random variable, called the confounder, that is a causal parent of both the observation $X_i$ and the outcome $Y_i$. We assume that the distributions of the confounder $U_i$ and the observation $X_i$ may change from one group to another. Equivalently, each group represents an intervention on the variables $X, Y, U$ such that the interventional distribution for group $i$ is $(X_i, Y_i, U_i) \sim P(do(X; \xi_i), Y, do(U; \zeta_i))$ where $\xi_i, \zeta_i$ are the unknown parameters controlling the interventions for group $i$. 

At test time, we receive a new set of $M$ observations $\{x'_i\}_{i=1}^M$ and the goal is to predict the the corresponding ground-truth outcomes $\{y'_i\}_{i=1}^M$. The ground-truth observation-outcome pairs were generated in 1 of 2 ways:

\begin{enumerate}
    \item The \textsc{Whole-Group} scenario. The testing data $\{(x'_i, y'_i)\}_{i=1}^M$ were sampled from a new interventional distribution $P(do(X; \xi'), Y, do(U; \zeta'))$ where $\xi', \zeta'$ are the unknown parameters controlling the new intervention. This scenario is equivalent to receiving a whole group of observations previously unseen during training.
    \item The \textsc{Single-Instance} scenario. Each pair of testing data $(x'_i, y'_i)$ was sampled from a different intervention $P(do(X; \xi'_i), Y, do(U; \zeta'_i))$ where $\xi'_i, \zeta'_i$ are the unknown parameters controlling the intervention for sample $i$. This scenario is equivalent to receiving a set of single instances of observations with no relationship to one another.
\end{enumerate}

\paragraph{Motivation.} This problem setup describes many real-world prediction problems in medicine and econometrics. One example is clinical risk modelling. Suppose we want to create a model that assesses a patient's risk of developing cardiovascular disease $Y$ based on the results of LDL cholesterol $X$. We train this model on patient case histories, where each observation-outcome pair $(X, Y)$ corresponds to one patient. The observation $X$ records that patient's level of LDL choloesterol following a test result and the outcome $Y$ records whether the patient developed cardiovascular disease in the 10 years following the test. The relationship between observation $X$ and outcome $Y$ is counfounded by many variables $U$, such as genetic predisposition, environment, etc. Typically, datasets of medical records are compiled with data sourced from different environments: different hospitals, countries, years, etc. Each of these environments corresponds to a different intervention on the joint distribution $P(X, Y, U)$.

\paragraph{Claim.} I claim that we can use the latent variables inferred by a \texttt{GID} model to achieve causally-robust predictions. To do this, we first train the \texttt{GID} model to autoencode each group $i$ of observations $\{x_{i,k}\}_{k=1}^{K_i}$ from the training set. For each group, the \texttt{GID} encoder will infer one group-level latent vector $\mathbf{s}_i \in \mathbb{R}^{D_S}$ and a group of instance-level latent vector $\{\mathbf{c}_{i,k}\}_{k=1}^{K_i}$ with $\mathbf{c}_{i,k} \in \mathbb{R}^{D_C}$. We model these latent codes as the random variables $C_i$ and $S_i$. If the disentanglement is successful, these random variables are independent: $\forall i \in \{1:N\}, ~ C_i \perp S_i$ (Assumption~\textit{I}).

Let's further assume that either one (but not both) of the instance variable $C_i$ or the group variable $S_i$ approximates the confounder $U_i$ (Assumption~\textit{II}). I will discuss later under what conditions this assumption is justified. Without loss of generality, let's assume that the group variable $S_i$ approximates the confounder $U_i$. By ``approximates'', I mean that the mutual information between the group variable $S_i$ and the confounder $U_i$ is equal to the entropy of the confounder $U_i$: $\forall i \in \{1:N\}, ~ I(U_i; S_i) = H(S_i)$.

There are two ways of using the inferred latent variables to learn a causally robust predictor, depending on which test-time scenario we are in, \textsc{Whole-Group} or \textsc{Single-Instance}:

\begin{enumerate}
    \item \textsc{Whole-Group}. This is the case when the testing data comes from a single group. We train the predictor $f_\theta: \mathbb{R} \times \mathbb{R}^{D_S} \to \mathbb{R}$ to model the outcome $Y_i$ as a function of the observation $X_i$ and the inferred group variable $S_i$: $Y_i = f_\theta(X_i, S_i)$. At test-time, we use the \texttt{GID} model to infer the group vector $\mathbf{s}'$ and use it alongside each observation $x'_k$ to predict each outcome $y'_k$: $\forall k \in \{1:K'\}, ~ y'_k = f_\theta (x'_k, s')$. The predictor function $f_\theta$ is causally robust because conditioning on the group variable $S_i$ is equivalent to closing the backdoor path $U_i$.
    \item \textsc{Single-Instance}. This is the case when the testing data comes from different groups. We use the instance variable $C_i$ as an instrumental variable to estimate the parameter $\theta$ of the predictor function $f_\theta: \mathbb{R} \to \mathbb{R}$. We first estimate the linear parameter $\gamma_X$ mapping the instance variable $C_i$ to the observation $X_i$ and then estimate the linear parameter $\gamma_Y$ mapping the instance variable $C_i$ to the outcome $Y_i$. The causal parameter $\theta$ will be equal to the ratio $\gamma_Y / \gamma_X$. At test-time, we predict each outcome $y'_k$ from $x'_k$: $\forall k \in \{1:K_i\}, ~ y'_k = f_\theta (x'_k)$. The instance $C_i$ is a valid instrumental variable because it is independent of the confounder $U_i$ due to Assumptions~\textit{I, II}.
\end{enumerate}

\begin{table}[t]
    \caption{How to use \texttt{GID} to achieve causally robust predictions.}
    \label{table:instructions}
    \begin{center}
    \begin{tabularx}{\columnwidth}{p{0.11\columnwidth}p{0.4\columnwidth}p{0.4\columnwidth}}
    \toprule & No intervention on $U$ & No intervention on $X$ \\
    \midrule {\sc Single-Instance} & Estimate the causal parameter $\theta$ using the inferred group-level latent variable $\mathbf{s}$ as instrument. & Estimate the causal parameter $\theta$ using the inferred instance-level latent variable $\mathbf{c}$ as instrument. \\ 
    \midrule {\sc Whole-Group} & Condition the predictor on the inferred instance variable $C_i$. & Condition the predictor on the inferred group variable $S_i$. \\
    \bottomrule
    \end{tabularx}{\parfillskip=0pt\par}
    \end{center}
\end{table}

\paragraph{Approximating the confounder.} When is it reasonable to assume that either one of the instance variable $C_i$ or the group variable $S_i$ approximates the confounder $U_i$? It depends on the relationship between the intervention on the confounder $do(U, \zeta)$ and the intervention on the observation $do(X, \xi)$. If the intervention on the observation $X$ is ``stronger'' than the intervention on the confounder $U$, then the inferred group-level latent variable $\mathbf{s}$ should be used as an instrumental variable . I define intervention ``strength'' on variable $X$ as the average KL-divergence between outcome variables from different groups when conditioned on $X$:

\[
    \sum_{1 \leq i \neq j \leq N} \mathbb{E}_{X_i, Y_i} \left[ \log \frac{P(Y_i | X_i)}{P(Y_j = Y_i | X_j = X_i)} \right] > \sum_{1 \leq i \neq j \leq N} \mathbb{E}_{U_i, Y_i} \left[ \log \frac{P(Y_i | U_i)}{P(Y_j = Y_i | U_j = U_i)} \right]
\]

\crit{[Maybe my definition of intervention ``strength'' is not great or necessary. If that's the case, let's skip over it.]}

At the extremes ends of the relationship between the intervention on the confounder $do(U, \zeta)$ and the intervention on the observation $do(X, \xi)$, we find two cases:

\begin{enumerate}
    \item \textbf{No intervention on $U$.} This is the case where the difference between groups is due solely to interventions on the observation $X_i$: $\forall 1 \leq i \neq j \leq N, ~ \mathrm{KL} [U_i ~||~ U_j] \approx 0$. In this case, the instance variable $C_i$ will approximate the confounder $U_i$ because $C_i$ captures the variation in the observation $X_i$ that is independent of the group. 
    \item \textbf{No intervention on $X$.} This is the case where the difference between groups is due solely to interventions on the confounder $U_i$: $\forall 1 \leq i \neq j \leq N, ~ \mathrm{KL} [X_i | U_i ~||~ X_j | U_j] \approx 0$. In this case, the group variable $S_i$ will approximate the confounder $U_i$ because $S_i$ captures the variation in the observation $X_i$ across groups.
\end{enumerate}

\paragraph{Contribution.} In this chapter, I provide an illustration for how the \texttt{GID} can achieve causally-robust predictions. I sketch some guidance for how to use the latent variables inferred by the \texttt{GID} in order to train a causally robust predictor (Table~\ref{table:instructions}). I then discuss two case studies showing how \textit{GID} can be applied on situations where either the observation $X$ or the confounder $U$ has been intervened upon.

\begin{table}[t]
    \caption{\textsc{Single-Instance} scenario results. Mean difference between the ground-truth $\beta$ and the estimate $\theta$. I report the standard deviation over 100 different dataset settings.}
    \label{table:single-instance-results}
    \begin{center}
    \begin{tabularx}{\textwidth}{lYYY}
    \toprule & \texttt{OLS} & \texttt{IV-Econ} & \textbf{\texttt{IV-GID}}\\
    \midrule No intervention on $U$ & $a \pm b$ & $a \pm b$ & $a \pm b$ \\
    \midrule No intervention on $X$ & $a \pm b$ & $a \pm b$ & $a \pm b$ \\
    \bottomrule
    \end{tabularx}{\parfillskip=0pt\par}
    \end{center}
\end{table}

\begin{table}[t]
    \caption{\textsc{Whole-Group} scenario results. Difference between the ground-truth $\beta$ and the estimate $\theta$. Mean Squared Error between ground-truth outcomes and predicted outcomes. I report the standard deviation over 100 different dataset settings.}
    \label{table:whole-group-results}
    \begin{center}
    \begin{tabularx}{\textwidth}{lYYY}
    \toprule & \texttt{OLS} & \texttt{IV-Econ} & \textbf{\texttt{IV-GID}}\\
    \midrule No intervention on $U$ & $a \pm b$ & $a \pm b$ & $a \pm b$ \\
    \midrule No intervention on $X$ & $a \pm b$ & $a \pm b$ & $a \pm b$ \\
    \bottomrule
    \end{tabularx}{\parfillskip=0pt\par}
    \end{center}
\end{table}

\section{Case 1: No intervention on $U$}

Suppose we want to measure the causal effect that the price of a product has on its demand. Let $Q_k = \alpha + \beta \cdot P_k + U_k$ be the function modelling the quantity sold of a given product $k$ given that it is sold at price $P_k$. The parameter we want to estimate is $\beta$. The confounder is $U_k$, which models the demand shocks on product $k$. For example, if the product is cake, the demand shock could be a change in VAT on cakes. The causal effect that we're interested in is the effect of a change in prices from $P_k$ to $P'_k$: $(Q_k (P_k) - Q_k(P'_k)) / (P_k - P'_k)$.

If we assume that the quantity sold is normally distributed, we can perform maximum likelihood via OLS to find the parameter $\beta$. However, this will be biased because $P_k$ is not independent of $U_k$.

We assume that the seller sets the price that maximises the profits, which are equal to price times the quantity minus the cost. The function mapping quantity to cost is $C_k (Q_k) = (c + V_k) \cdot Q_k$. 

The profit is equal to $\Pi_k = P_k \cdot Q_k - C_k$. The profit is maximised with respect to price $P_k$ when $P_k = \frac{1}{2} \left( c + V_k - \frac{\alpha + U_k}{\beta} \right)$. The equations are:

\[
    Q_k = \alpha + \beta \cdot P_k + U_k
\]
\[
    C_k = (c + V_k) \cdot Q_k
\]
\[
    P_k = \frac{1}{2} \left(c + V_k - \frac{\alpha + U_k}{\beta} \right)
\]

Let's say we just perform OLS regression on the data. The implied model for price given the demand is $Q_k = \mu + \gamma \cdot P_k + \nu$. 

\paragraph{Dataset.}

\draft{\paragraph{\textsc{Single-Instance} scenario.} We run an experiment to estimate the parameter $\beta$. We generate a few  datasets by randomly sampling values for the parameters $\alpha, \beta, \gamma$. We then use OLS to estimate the parameters, and show that the estimate is consistently biased. We then use two methods for instrumental variable regression. One is the conventional method of using another variable in the group as an instrument. The other is to use the latent representation of the whole group as an instrument. We show that the confidence interval that we get is tighter.}

\draft{\paragraph{\textsc{Whole-Group} scenario.} We run an experiment to estimate the parameter $\beta$. We generate a few  datasets by randomly sampling values for the parameters $\alpha, \beta, \gamma$. We train our predictor conditioned on }

\section{Case 2: No Intervention on $X$}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% References:
%%
% If you include some work not referenced in the main text (e.g. using \nocite{}), consider changing "References" to "Bibliography".
%

% \renewcommand to change default "Bibliography" to "References"
% \renewcommand{\bibname}{References}

% \bibliography{main,phd_thesis}
\bibliographystyle{plain}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Appendix:
%%

%\appendix

%\chapter{Extra Information}

\end{document}
