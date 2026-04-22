# ResearchMind

I built ResearchMind to help PhD students and researchers discover and analyze academic papers faster. Instead of manually searching across multiple databases, you send a topic and citation range and the system pulls papers from ArXiv and OpenAlex, filters them, and returns a structured list with summaries. You can then deep dive into any individual paper and get a detailed AI analysis covering limitations, improvements, and future research directions.

## Why I built this

Researchers waste hours searching across ArXiv, Google Scholar, and other databases for relevant papers. I wanted a single workflow that queries multiple sources simultaneously, filters by citation count, and uses an AI agent to surface only the most relevant results with proper context.

## How it works

The system has two separate n8n workflows.

The Paper Discovery workflow receives a topic and citation range via webhook, queries ArXiv and OpenAlex simultaneously, merges and decodes the results, then passes everything to a Groq powered AI Agent that filters and formats the papers into a clean structured list.

The Deep Dive workflow receives a single paper's details via webhook and uses a Groq powered AI Agent to produce a detailed analysis covering methodology limitations, suggested improvements, future research directions, and alternative methods to try. Written specifically for PhD level readers.

## Tech Stack

n8n for workflow automation, ArXiv API and OpenAlex API for paper data, Groq with Llama 4 Scout for AI analysis, and JavaScript for abstract decoding.

## How to Import the Workflows

Open n8n, click Add Workflow, select Import from File, and import both workflow files one at a time. Then go to Credentials in n8n and add a Groq API credential using your Groq API key from console.groq.com. Assign the credential to the Groq Chat Model node in both workflows.

## Example Payload

Paper Discovery:

{
  "topic": "transformer attention mechanisms",
  "min_citations": 50,
  "max_citations": 5000
}

Deep Dive:

{
  "title": "Attention Is All You Need",
  "authors": "Vaswani et al.",
  "year": "2017",
  "citations": "90000",
  "source": "ArXiv",
  "abstract": "We propose a new simple network architecture..."
}

## Notes

PubMed and Semantic Scholar nodes are included in the Paper Discovery workflow but disabled by default. They can be enabled if you want broader coverage across medical and scientific literature.
