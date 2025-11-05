\documentclass[11pt]{article}

\usepackage{mathpazo}
\usepackage[natbib,style=alphabetic,maxalphanames=3,maxcitenames=2,maxbibnames=10]{biblatex}
\addbibresource{bibliography/bib.bib}

\usepackage[margin=1in]{geometry}
\usepackage{amsmath,amssymb,amsthm}
\newtheorem{definition}{Definition}

\usepackage{todonotes}
\usepackage{xcolor}
\usepackage{color-edits}
\usepackage[colorlinks,citecolor=blue,linkcolor=blue,urlcolor=blue]{hyperref}

% matan includes
\usepackage{outlines}				%out enviroment 
\usepackage{xspace}                 %so we don't need
\usepackage{cancel}                 %\not across multiple symbols
\usepackage{mdframed}
\usepackage{enumitem}               % nolistsep
\usepackage{cleveref}               % cref

\include{lib/macros.tex}

\title{CASI--MATS 0: Application}
\author{Allan Fang}
\begin{document}
\maketitle

% \begin{abstract}
%     This is a very good paper.
% \end{abstract}

\section{The application}




\subsection{Technical questions regarding projects}




\subsubsection{Evidence for LM WMDP capabilities}
\cite{gotting2025virology} proposes a benchmark for evaluating LLMs' virology capabilities.
Read the paper and assess it critically: Do you see any methodological gaps or limitations that would make you doubt their results?
What findings did you find most striking or concerning?  

An assumption that the article makes, is that scientists gaining more knowledge about virology would be able to carry out experiments better, which isn't necessarily true. Although, on paper 
a scientist knowing more knolwedge about a specific field should lead to an increase in a scientist's ability to carry out experiments. But in reality, only a certain degree of knowledge and 
practical understanding is needed in order to properly carry out the experiments. Therefore, the extra information provided by LLM's isn't "essential" or "needed" for scientist's to perform 
their tasks.

I found it concerning that there was a lack of experts verifying each question. They intended to have 3 experts on each question, but 65 questions were only answered by two experts,
9 questions by only one expert, and 19 questions could not be covered by the baselining. So this could lead to more inaccuracy in the correctness of each question.

A finding that I found to be concerning, is how much higher OPENAI's LLM performed (43.8%) on the VCT compared to expert virologists(22.1%)

Another concerning fact is that of all submitted questions there were 1, 042 total reviews, and only 72.6% approved the question, while a large amount of 27.4% disapproved. This 
makes me concerned as to how many disapproving reviews there were.


\subsubsection{Getting familiar with the threat model}
\cite{jones2024adversariesb} proposes a threat model that differs from traditional jailbreaking works like \cite{chao2024jailbreakinga}.
What is the key difference?
Now, try implementing the attack from \cite{jones2024adversariesb} on one or two models and report your results.
Explain the broad attack framework, what you tried, and your reasoning behind your approach. 
Explain how you assessed whether you succeeded or not.


I used Chat-GPT 5 as my frontier model, and I used BLOOM-560M and MPT-1B as my weaker open source models. I used both weaker source models to prompt ChatGPT-5 
to create context for prompts to generate hate speech. My reasoning is that BLOOM-560M and MPT-1B are both weaker models, so they would be more open to creating prompts
that would indicate or signify hate speech as a result. While ChatGPT-5 would be more open to give context and strong information for the background of hate speech prompts.
As a result ChatGPT-5 would supply more infomration to the weaker models to create stronger hate speech prompts. 

My result was that ChatGPT-5 continuosly gave information, but the weaker models could not create a prompt to exploit ChatGPT-5 to create hate speech. Therefore, I think that 
the idea is correct, but the implementation and execution could've been improved. 


The key difference is that the traditional jailbreaking would use an LLM to generate prompts to another LLM to get the second LLM to produce a jail break.
While the non traditional method, uses multiple LLM's to each do a subtask of a jail break, and combining these multiple LLM's would produce a jailbreak.


\subsubsection{Assessing another paper on the same topic}
\cite{glukhov2024breach} is another paper on decomposition attacks.
What unique value does it add beyond previous work?
Can you explain what in your opnion their mathematical framework accomplishes?

One value is the significance of a model "leaking" sensitive information even the when the model didn't produce direct harmful content.
The second value is to try to gain small bits of "leaked" sensitive info from the a model through sub questions, in order
to result in getting the answers to an actually harmful question.

Their mathematical framework allows researchers to quantify the amount of impermissable information being leaked. 

\subsubsection{Curating data}
\cite{brown2025benchmarking} curates a dataset to study decomposition attacks, focusing exclusively on WMDP queries.
Your task: build a small cyber dataset for decomposition attacks.
Explain your methodology for curating the dataset---why did you choose this approach and how you chose this approach?
How would you scale it up?
Can you get an agent to try to solve these questions directly? With decomposition attack? 

So basically the idea is to make a small dataset to study how decomposition attacks work, but in a safe, cyber-ish way. 
I’d start by picking a few tasks that are kinda like security problems but won’t actually let anyone hack anything, 
like writing code that could have a vulnerability, or a script with messed-up permissions, or spotting sketchy links 
in a fake phishing scenario. Then for each task, I’d break it down into smaller, harmless sub-tasks that the model could 
answer without refusing, like asking it to show a Python function that takes input, explain why not checking input is bad,
and then show the safe way to do it. That way, we can see if the model could get tricked into combining the answers in a 
way that sort of reproduces the unsafe idea, without actually doing anything dangerous. I’d annotate stuff like what kind 
of task it is, how many sub-questions there are, and what the expected answers look like. For scaling up, you could add 
more base tasks like network configs or different programming languages, maybe even let a model suggest decompositions 
and then filter them for safety. Then you could test an agent by giving it the full prompt first, which it’d probably 
refuse, and then feed it the sub-tasks one by one to see if it can piece them together and kind of solve the bigger
task, again just safely, like showing reasoning or patterns without producing anything harmful. For the dataset itself, 
I’d keep it small at first, maybe 5–10 tasks with 2–5 sub-tasks each, and for each I’d have the full task, the sub-tasks,
and the expected outputs, so we can track how well decomposition works.

\subsubsection{Literature search}
Hunt for other relevant papers on decomposition attacks and multi-context jailbreaking.
What did you find?
If you can't find more paper, which papers other topics do you consider closely related?

Paper 1: DrAttack: Prompt Decomposition and Reconstruction Makes Powerful LLMs Jailbreakers 

This paper introduces a method called DrAttack which decomposes a malicious prompt into multiple sub‑prompts, and
then reconstructs the prompt to hide the malicious intent from the model’s safety filters. It uses decomposition, 
reconstruction, and "synonym search" which repalces words with synonyms to hide the intent.
“Synonym Search”: replace key words or phrases with synonyms to further obfuscate the intent.

Paper 2 Prompt Packer: Deceiving LLMs through Compositional Instruction with Hidden Attacks (Jiang et al., 2023)

This paper introduces Compositional Instruction Attacks (CIA), where the attacker embeds harmful instructions 
inside regular looking composite tasks so that the LLM fails to detect the malicious intent. There are two 
transformation methods: T‑CIA and W‑CIA. They disguise harmful instructions as seemingly harmless tasks 
so that the model accepts them. 

It highlights a subtle attack vector where the malicious intent is hidden in composite or multi‑intent instructions, 
showing that detection of harmful content must account for underlying intent, not only surface content. 


\subsubsection{Future work}
What excites or concerns you about this line of work?

I think that AI will be a tremendous talking point from now until the future. As AI's usage grows, so too does the concern for its security and safety. 
I'm excited to see how we could manage the capabilities of AI to not only provide information to the public, but also to not provide harmful information.
I also really like working with AI, and learning about the unique and niche nitty gritty aspects of AI through research papers too. Researching 
AI safety also creates a lot of real world applications for applying the research on improving AI. So it's really exciting to see how meaninful AI safety 
work is, and how directly applicable AI safety is. I also believe AI safety is a topic that isn't as well researched as AI. So there are a lot of new 
discoveries that could be made on AI safety even for a potential new researcher like me. Lastly, I've been reading AI research papers but I have yet to 
properly apply my learnings and my knowledge to an actual project that will impact others. So I would be very excited and committed to learning and working
on AI Safety.

Some concerns I have about AI safety itself, is how big tech may interfere with our work and research. AI safety calls for the regulation of AI research
in order to double check their work and create limitations on their work also. So research on AI safety could either be ignored or hindered by the influence
of big tech, which is a great safety concern for the world and for the tech industry. SEeing the world trying to advance so rapidly towards AGI and "superhuman" 
AI does slightly worry me that no one sees the possiblity of our planet being turned into a dystopian fantasy world that is overrun by AI. 

What questions do you have about its real-world impact?

Some questions I have, is how how much influence does AI safety have on the rapid growth of AI research?
How would we be able to ensure AI safety in current AI's being researched and created?
Would AI safety be able to play a significant role in the highly prioritized field of AI Research?

What future directions seem most promising?

I think that AI safety's future in regulating AI is uncertain due to big tech and the government disallowing too many regulations.
While I think AI safety's future is in helping users and the general public be weary of the dangers of AI. I think that once the public
is more educated about the dangers of AI, the public themselves may take action and influence the government and big tech to regulate
AI better. I mainly think that AI research is beneficial and important to educating users, and educating the general public on the 
dangers of AI and AI itself.

This is your space to share your unfiltered thoughts---just try to stay on topic $\;$ ; )

% \subsection{Soft questions}
% Answer the following questions in $\approx$ a paragraph each.
% \begin{enumerate}
%     \item Why do you want to participate in this project? 
%     \item We hope to select students for the project who will actually have the capacity to participate and think that $\approx$ 10 hrs / week is required to make this experience meaningful. We expect that you are already very, very, very busy. Please concretely explain how you plan to make time for this project and when you expect to be able to work on it? 
%     \item Are there any specific experiences you have that you want us to consider with your application?  
% \end{enumerate}

\end{document}
