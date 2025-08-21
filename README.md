
# Revit Licensing Optimizer — Interactive App

A Streamlit web app to optimize the mix of Autodesk Revit named-user seats and Flex tokens.
Built for easy "what-if" analyses and executive-friendly visuals.

## Quickstart (Docker)

```bash
# 1) Build
docker build -t TST .

# 2) Run
docker run --rm -p 8501:8501 revit-licensing-optimizer

# 3) Open
# Visit http://localhost:8501 in your browser
```

## Direct (no Docker)
```bash
pip install -r requirements.txt
streamlit run TST.py
```

## What it does
- Lets you enter team size and usage cohorts (heavy/medium/light authors)
- Adjust seat price, token price, tokens per day, and buffer
- Compares three strategies:
    1. **Lean**: seats for heavy; medium+light on Flex
    2. **Balanced**: seats for heavy+medium; light on Flex
    3. **Max**: all authors get seats (with a tiny Flex burst reserve)
- Shows the **cheapest** option and the break-even days per user
- Optional **price sensitivity grid** for multiple price points

## Notes
- Default assumptions: 300 employees, 50 projects, 90/40/20 heavy/medium/light authors with 220/150/40 days.
- Flex consumption default: 10 tokens/day/user with a 10% buffer.
- Break-even days ≈ `seat_price / (10 × token_price)`

## Customize
- Edit `TST.py` to change formulas or add more scenarios.
- If you have real usage logs, replace inputs with a CSV uploader and compute cohort sizes automatically.

## Security & Networking
- The app runs read-only analytics; it stores nothing server-side.
- To share inside your network, deploy the Docker container to an internal host and reverse-proxy behind HTTPS.
