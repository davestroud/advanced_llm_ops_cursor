---
name: figure-rules
description: Rules for creating figures in the book.
---

# Overview

% ----------------------------------------------------------------------
% FIGURE: Inputs taxonomy (cleaned; removed trailing comma; simplified arrows)
% Preamble requirements (once): \usepackage{tikz,adjustbox} and
% \usetikzlibrary{arrows.meta,positioning,fit,calc}
% ----------------------------------------------------------------------
\begin{figure}[t]
\centering
\begin{llmfigbox}
\begin{tikzpicture}[
  font=\small,
  cNews/.style  ={fill=blue!18,  draw=blue!55!black},
  cNGO/.style   ={fill=teal!18,  draw=teal!55!black},
  cSocial/.style={fill=purple!16,draw=purple!60!black},
  cHealth/.style={fill=orange!18,draw=orange!65!black},
  hub/.style    ={draw=black!25, rounded corners=5pt, fill=black!2},
  bubble/.style ={circle, minimum size=14mm, inner sep=2pt, line width=0.6pt, align=center},
  arrowthin/.style={-{Stealth[length=2mm,width=1.6mm]}, line width=0.5pt},
  note/.style   ={font=\small, align=left, text=black!70}
]

\node[hub, minimum width=90mm, minimum height=50mm] (group) {};
\node[black!50, font=\small] at ([yshift=-6pt]group.north) {Curated external evidence (ingested and vetted)};

\node[bubble,cNews]   (news)   at (-2.8,  1.1) {News wires\\\& reports};
\node[bubble,cNGO]    (ngo)    at ( 0.0,  1.7) {NGO bulletins};
\node[bubble,cSocial] (social) at (-3.0, -1.0) {Social media\\(vetted)};
\node[bubble,cHealth] (health) at ( 0.4, -1.6) {Public health\\\& infrastructure};

\draw[black!10, line width=2pt] (news) -- (ngo);
\draw[black!10, line width=2pt] (news) -- (social);
\draw[black!10, line width=2pt] (social) -- (health);
\draw[black!10, line width=2pt] (ngo) -- (health);

\node[draw=black!30, fill=black!4, rounded corners=3pt, inner sep=3pt,
      minimum width=22mm, minimum height=8mm] (funnel) at (1.5, 0.1) {RAG retrieval};

\node[draw=black!60, rounded corners=4pt, fill=black!1, minimum height=9mm,
      inner sep=4pt, align=center] (journalist) at (4.5, 0.1)
      {\textbf{Journalist queries}\\\scriptsize (questions and tasks)};

\draw[arrowthin] (news.east)   -- (funnel.west);
\draw[arrowthin] (ngo.east)    -- (funnel.west);
\draw[arrowthin] (social.east) -- (funnel.west);
\draw[arrowthin] (health.east) -- (funnel.west);
\draw[arrowthin] (funnel.east) -- (journalist.west);

\node[note, anchor=north west] at ([xshift=4pt,yshift=-4pt]group.south west) {%
\textbf{Inputs:} curated sources are ingested, normalized, and embedded.\\
\textbf{Flow:} sources $\rightarrow$ retrieval $\rightarrow$ journalist-facing answers.};

\end{tikzpicture}
\end{llmfigbox}
\caption{Evidence source selection determines RAG quality and trustworthiness. \ishtar{} curates inputs from news wires, NGO bulletins, vetted social media, and public health \& infrastructure feeds, ensuring reliable, authoritative sources. This curation strategy demonstrates how source quality directly impacts answer accuracy and citation fidelity in production RAG systems.}
\label{fig:ch01_ishtar_inputs_taxonomy}
\end{figure}
