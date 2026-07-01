Chinese Court Verdict Sentiment Analyzer

I'm an undergraduate student majoring in Political Science and International Studies with a focus on East Asia, and this summer I decided to combine that with something I'm completely new to, but have found an inate passion for — artificial intelligence and data science. This project is the result of that intersection.

My research focuses on the influence of public opinion in the Chinese judicial court system. More specifically, verdict analysis done through the framing and the language choices judges make when describing defendants, victims, and evidence.


Project Scope

This is a natural language processing (NLP) pipeline that analyzes 500 real criminal court cases published by China's Supreme People's Court. Using Python to built a system that reads Chinese legal text, it breaks it down word by word and scores each case for four types of judicial language: state authority framing, leniency signals, defendant-negative language, and defendant-positive language.

I created visuals to depict those patterns across different charge types and see the language judges use, which varied depending on the sensitivity of the case. I was also able to examine whether that variation might explain something about how public pressure shapes judicial behavior.

This project is part of a broader research agenda I'm developing toward a peer-reviewed publication comparing judicial language across several East Asian countries and the United States.


Purpose

China's judicial system sits at a really interesting intersection of law, politics, and public opinion. On paper, courts are supposed to be independent. In practice, scholars have documented significant pressure on judges from state actors, party officials, and increasingly, the public. High-profile cases attract media attention and online outrage, and there's real evidence that this affects outcomes.

But most of the research on this question has been qualitative — reading individual cases, interviewing lawyers, analyzing policy documents. What I wanted to know is whether you can detect these pressures computationally, at scale, in the language of the verdicts themselves. That felt like a genuinely new angle, and it's the question driving everything in this repo.


The Data


Source: CAIL2018 — Chinese AI and Law Challenge Dataset
Published by: China's Supreme People's Court, hosted on Hugging Face for academic research
Sample: 500 criminal cases (random sample from the training set)
Key fields:

fact — the actual case description text in Chinese
accusation — the charge (e.g., intentional injury, theft, weapons possession)
imprisonment — sentence length in months
death_penalty / life_imprisonment — severity indicators





This is real court data from real cases. The defendants are anonymized (referred to as 某某, a Chinese placeholder equivalent to "John Doe"), but the facts, charges, and sentences are genuine.


What I Found

These are preliminary findings based on 500 cases. I'm expanding the dataset and adding sentiment modeling, but here's what the data shows so far:

The most striking finding: weapons possession cases (非法持有枪支) are dominated almost entirely by state authority language, with virtually no leniency framing appearing across any of the cases in that category. By contrast, intentional injury cases (故意伤害) show a genuinely complex mix of all four language types — including notable leniency signals and defendant-positive framing.

What that might mean: Chinese courts appear to use significantly more state-centered, authoritative language in politically sensitive cases (like weapons) compared to more common cases like injury or theft. This could reflect the political stakes around weapons charges in China — or it could reflect judges writing defensively in cases they know will attract scrutiny.

The leniency puzzle: When I plotted leniency language against sentence length, there was no clean correlation. Cases with high leniency keyword scores still received long sentences, and vice versa. This suggests judges may use mitigating language as procedural formality regardless of the actual outcome — which is itself an interesting finding about how Chinese judicial writing works.

FindingDetailMost common term被告人 ("defendant") — 2,149 hits across 500 casesVictim vs. defendant language ratio被害人 appears at ~60% the rate of 被告人Highest state authority languageWeapons possession cases by a significant marginMost linguistically complex casesIntentional injury — all four categories activeLeniency-sentence correlationWeak — leniency language does not predict shorter sentences


How I Built This

I came into this project as a complete beginner in programming. I had never opened a terminal before starting this work. Here's what the pipeline actually does:

1. Data loading — I pulled 500 cases directly from the CAIL2018 dataset using Hugging Face's datasets library, which lets you stream a small sample from a 2.6 million case corpus without downloading gigabytes of data.

2. Chinese text tokenization — Chinese doesn't use spaces between words, so before any analysis you need a tokenizer. I used jieba, the standard Chinese NLP library, with a custom stopword list to filter out procedural filler words.

3. Word frequency analysis — I counted the most common words across all 500 cases to understand what language dominates Chinese criminal verdicts. The results are heavy on state-centered procedural language: prosecution, evidence, government organs, forensic assessment.

4. Keyword scoring — I built a hand-curated dictionary of four judicial language categories and scored every case against it. This is my baseline method before applying machine learning.

5. Visualization — All charts are built in Plotly and are fully interactive — you can hover over bars and points to see exact values.


How to Run This Yourself

bash# Clone the repo
git clone https://github.com/shriadev/china-verdict-sentiment

# Install dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook 01_exploration.ipynb


What's Coming Next


 Sentiment classification using a pretrained Chinese BERT model
 Expand dataset to 2,000–3,000 cases for stronger statistical validity
 Add Japan Supreme Court data for cross-system comparison
 Draft research paper for undergraduate journal submission
 Submit abstract to Midwest Political Science Association (MPSA)



Technologies Used

ToolWhat I Used It ForPython 3.14EverythingpandasData manipulation and analysisjiebaChinese text tokenizationHuggingFace datasetsStreaming the CAIL2018 datasetPlotlyInteractive chartstransformersSentiment modeling (in progress)


About This Project

This is independent undergraduate research in international politics and computational social science. I'm working toward a peer-reviewed publication on public opinion and judicial behavior in China, with a planned comparative extension to Japan, South Korea, and the United States.

I'm very new to both coding and academic publishing, but I believe that's not a reason to aim small. If you're a researcher working on related questions, I'd genuinely love to connect.

Shria Dev
GitHub: @shriadev
