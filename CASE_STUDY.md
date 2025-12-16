# I built a local AI Compliance Officer because my database had 2.4% garbage data.

**How I used `bart-large-mnli` and Compliance-as-Code to audit a directory of 400+ businesses without a legal team.**

## The Problem: "Drift" is Liability

I run a niche directory for regulated service providers (Lawyers, Consultants, and Tax Advisors).

In the world of EU AI Regulation and general liability, classifying these businesses is high stakes. If my database says a "Logistics Company" is a "Lawyer," and a user relies on that, it is a potential liability.

I scraped 416 listings. I thought the data was clean.
I was wrong.

## The Naive Solution: Manual Review
I could have manually checked 416 rows.
* **Pros:** 100% human verification.
* **Cons:** Boring, slow, and unscalable.

## The Engineer's Solution: TagGenie 🧞
I built a local CLI tool using `transformers` and `facebook/bart-large-mnli` (Zero-Shot Classification). No OpenAI API, no data leakage. Just local silicon.

I ran it on my dataset with a specific goal: **Audit the existing tags.**

The model runs locally on my CPU. It took 18 minutes (~23 rows/minute).

## The "Compliance" Logic (The Secret Sauce)
Most developers stop at `print(prediction)`. But "Prediction" isn't "Compliance."

I treated this like a **High-Risk AI System**. I implemented a strict **Compliance Policy** in Python:

1.  **The "Safety Valve":** If the input text is empty or garbage, default to "None." (Don't hallucinate).
2.  **The Confidence Threshold:**
    * **< 50%:** Flag for Human Review. (The AI is unsure).
    * **> 85%:** Auto-Fix. (The AI is certain the original data is wrong).
    * **Else:** Trust the Original.

## The Results: The "Danger Zone"
The audit revealed exactly why "Compliance as Code" is necessary.

* **Total Rows:** 416
* **Agreement Rate:** 55.5% (The AI and I agreed mostly).
* **Low Confidence (<50%):** 230 rows flagged for human review.

**But here is the kicker:**
The AI found **10 rows (2.4%)** in the "Danger Zone."
These were rows where the Original Data said X, but the AI was **95% sure** it was Y.

**Example 1:**
* **Business:** "Generic Logistics Co"
* **Original Tag:** `Finance & Tax` (???)
* **AI Prediction:** `Relocation Services` (95% Conf)
* *Verdict:* The AI was right. The scrape was wrong.

**Example 2:**
* **Business:** "Generic Law Firm"
* **Original Tag:** `Finance & Tax`
* **AI Prediction:** `Legal Services` (89% Conf)
* *Verdict:* The AI was right.

## The Audit Trail
To prove my tool is compliant, I didn't write a Word doc. I used [Compli-AI](https://github.com/compli-ai/compli-ai) to scan the codebase and generate an automated inventory.

**Command:**
`$ compli-ai scan`

**Output:**
```text
Scanning directory: ./tag-genie...
Scan complete. Found 6 Python file(s).

Detected Python
   Libraries
┏━━━━━━━━━━━━━━┓
┃ Library      ┃
┡━━━━━━━━━━━━━━┩
│ rich         │
│ transformers │
│ typer        │
└──────────────┘

Detected AI Models
┏━━━━━━━━━┳━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ File    ┃ Line ┃ Model Name/Class         ┃ Framework               ┃
┡━━━━━━━━━╇━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ main.py │ 35   │ facebook/bart-large-mnli │ Hugging Face (Pipeline) │
└─────────┴──────┴──────────────────────────┴─────────────────────────┘
```

This isn't just a log. This is the beginning of my Technical Documentation for the EU AI Act (Annex IV).

## Conclusion: Why I built Compli-AI
Building the AI agent (`TagGenie`) was the easy part. Building the Guardrails—the confidence checks, the risk thresholds, the audit logs—that was the hard part.

That is why I am building Compli-AI. It is an open-source tool to treat AI Compliance as Code. It scans your project, maps your dependencies, and helps you generate the Technical Documentation required by the EU AI Act.

**Links:**
* [Compli-AI on GitHub](https://github.com/compli-ai/compli-ai)

