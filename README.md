Chinese Court Verdict Sentiment Analyzer

I am an undergraduate student majoring in Political Science and International Studies with a focus on East Asia, and this summer I decided to combine my studies with something I am completely new to, but have found an inate passion for: artificial intelligence and data science. This project is the result of that intersection.

My research focuses on the influence of public opinion in the Chinese judicial court system. More specifically, verdict analysis done through the framing and the language choices judges make when describing defendants, victims, and evidence.


Project Scope

This is a natural language processing (NLP) pipeline that analyzes 500 real criminal court cases published by China's Supreme People's Court. Using Python to built a system that reads Chinese legal text, it breaks down data word by word and scores each case for four types of judicial language: state authority framing, leniency signals, defendant-negative language, and defendant-positive language.

I created visuals to depict those patterns across different charge types and see the language judges use, which varied depending on the sensitivity of the case. I was also able to examine whether that variation might explain something about how public pressure shapes judicial behavior.


Purpose

China's judicial system sits at a really interesting intersection of law, politics, and public opinion. On paper, courts are supposed to be independent. In practice, scholars have documented significant pressure on judges from state actors, party officials, and increasingly, the public. High-profile cases attract online attention, and there is real evidence that this affects outcomes.

But most of the research on this subject has been qualitative — reading individual cases, interviewing lawyers, analyzing policy documents. What I wanted to know is whether you can detect these pressures computationally, at scale, in the language of the verdicts themselves. That felt like a genuinely new angle, and it's the question driving everything in this repo.

So all in all, my research question is: How does public opinion influence judicial language and sentencing outcomes in China's criminal court system and does that influence vary by charge type, case sensitivity, or regional context? 


The Data

Source: CAIL2018 — Chinese AI and Law Challenge Dataset
Published by: China's Supreme People's Court, hosted on Hugging Face for academic research
Sample: 500 criminal cases (random sample from the training set)
Key fields:

Fact — the actual case description text in Chinese
Accusation — the charge (e.g., intentional injury, theft, weapons possession)
Imprisonment — sentence length in months
Death_penalty / Life_imprisonment — severity indicators

This is real court data from real cases. The defendants are anonymized (referred to as 某某, a Chinese placeholder equivalent to "John Doe"), but the facts, charges, and sentences are genuine.


What I Found

These are preliminary findings based on 500 cases. I will be expanding the dataset and adding sentiment modeling, but here's what the data shows so far:

The most prevalent finding: weapons possession cases (非法持有枪支) are dominated almost entirely by state authority language, with almost no leniency framing appearing across any of the cases in that category. By contrast, intentional injury cases (故意伤害) show a complex mix of all four language types, including leniency signals and defendant-positive framing.

What that might mean: Chinese courts appear to use significantly more state-centered, authoritative language in politically sensitive cases (like weapons) compared to more common cases like injury or theft. This could reflect the political stakes around weapons charges in China, or how judges write defensively in cases they know will attract scrutiny.

The leniency puzzle: When I plotted leniency language against sentence length, there was no clear correlation. Cases with high leniency keyword scores still received long sentences, and vice versa. This suggests judges may be using mitigating language as procedural formality regardless of the actual outcome, which is an interesting finding about how Chinese judicial writing works, itself.

Finding Details

Most common term 被告人 ("defendant") — 2,149 hits across 500 cases
Victim vs. defendant language ratio 被害人 appears at ~60% the rate of 被告人 
Highest state authority language 
Weapons possession cases by a significant margin 
Most linguistically complex cases
Intentional injury — all four categories active
Leniency-sentence correlation
Weak — leniency language does not predict shorter sentences


How I Built This

1. Data loading: I pulled 500 cases directly from the CAIL2018 dataset using Hugging Face's datasets library, which lets you stream a small sample from a 2.6 million case corpus without downloading gigabytes of data.

2. Chinese text tokenization: Chinese doesn't use spaces between words, so before any analysis a tokenizer was needed. I used jieba, the standard Chinese NLP library, with a custom stopword list to filter out procedural filler words.

3. Word frequency analysis: I counted the most common words across all 500 cases to understand what language dominates Chinese criminal verdicts. The results are heavy on state-centered procedural language: prosecution, evidence, government organs, forensic assessment.

4. Keyword scoring: I built a hand-curated dictionary of four judicial language categories and scored every case against it. This is my baseline method before applying machine learning.

5. Visualization: All charts are built in Plotly and are fully interactive — you can hover over bars and points to see exact values.


How to Run This Yourself

bash# Clone the repo
git clone https://github.com/shriadev/china-verdict-sentiment

# Install dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook 01_exploration.ipynb


Technologies Used

This project was built using Python 3.14 as the core programming language, with pandas handling all data manipulation and cleaning, and jieba performing Chinese text tokenization. I loaded the CAIL2018 Supreme People's Court dataset using HuggingFace's datasets library, which allowed me to stream a manageable sample from a 2.6 million case corpus. All interactive charts and visualizations were built using Plotly, and sentiment modeling using a pretrained Chinese BERT model via the transformers library is currently in progress. Throughout development I used Claude, an AI assistant by Anthropic, as a debugging tool. All analytical decisions, research design, keyword dictionaries, interpretation of findings, and written analysis are entirely my own, and AI assistance is disclosed here in the interest of full transparency.


About This Project and What's Coming Next

This project is the foundation of what I intend to become a peer-reviewed, published article and eventually, a comparative study spanning different East Asian Countries and the United States. Although I am rather new to the world of computational research and political science, I am committed to seeing this work coming become something special. 

If you are a professor, conference reviewer, or researcher working on questions related to Chinese law, judicial behavior, or computaational social science, I welcome feedback, collaboration, and mentorship. Thank you. 

Shria Dev
GitHub: @shriadev
