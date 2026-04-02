# Examples

Real-world usage examples showing the pipeline in action.

---

## Example 1: Thread Only (Casual Discussion)

### Input
```
/reddit

r/Entrepreneur

Title: What's the one thing you wish you knew before starting your business?

Body: Pretty self-explanatory. Starting a small e-commerce business next month 
and want to learn from your mistakes. What would you tell your younger self?
```

### Pipeline Trace
```
Stage 1: Format 1 (thread only), no operator instructions
Stage 2: Overwhelmed Novice (3/5 signals) + Validation Seeker (2/5)
         Primary: Overwhelmed Novice
Stage 3: Beginner (vague, no prior attempts, asks open-ended)
         Emotion: Excited
         Personality: I (Influential, story-seeking)
Stage 4: No gates triggered
Stage 5: Skip (no factual claims to verify)
Stage 6: Skip (casual post, not complex)
Stage 7: Length = 2-3 sentences (casual discussion thread)
Stage 8: Domain = E-commerce (loads domain-brain)
Stage 9: Quality gate pass
Stage 10: Output
```

### Output
```
Your customers will tell you what to sell if you shut up and listen. 
Most first-time e-commerce founders spend 3 months perfecting their 
store and zero hours talking to the people who'd actually buy from 
them. Talk to 20 potential customers before you spend a dollar on 
inventory.
```

---

## Example 2: Thread + Comments (Adding What's Missing)

### Input
```
/reddit

r/SaaS

Title: My SaaS has been stuck at $3K MRR for 6 months. What am I doing wrong?

Body: I launched 8 months ago, hit $3K MRR in 2 months, and haven't grown since. 
I've tried content marketing, cold outreach, and a referral program. Nothing moves 
the needle. Product has good reviews, 4.5 stars. Churn is about 8% monthly. 
I'm a solo founder spending about 60 hours a week on this.

---

Comments:

u/saas_veteran (142 upvotes): Have you talked to the customers who churned? 
That 8% monthly churn is killing you. At that rate you're replacing your entire 
customer base every year.

u/growthguy (89 upvotes): What's your pricing? $3K MRR could mean 30 customers 
at $100 or 300 at $10. Very different problems.

u/indie_maker (45 upvotes): 60 hours a week as a solo founder is a recipe for 
burnout. Are you spending those hours on growth or on support/maintenance?

u/marketing_pro (28 upvotes): Content marketing takes 6-12 months to show results. 
You might just need to be patient.
```

### Pipeline Trace
```
Stage 1: Format 2 (thread + 4 comments)
         Comment map: churn, pricing, time allocation, content marketing patience
         Average comment length: 2-3 sentences
         Thread energy: analytical, supportive
Stage 2: Sunk Cost Prisoner (2/5) + Burnout Denier (3/5)
         Primary: Not a clean match; using compound rules
Stage 3: Intermediate (specific metrics, tried multiple channels)
         Emotion: Frustrated (6 months stuck)
         Personality: C (Conscientious, data-driven)
Stage 4: No gates triggered
Stage 5: Run math: 8% monthly churn = 96% annual, ~61% annual retention
Stage 6: Loads cognitive-engine
         Prior: Plateaued SaaS, base rate says churn is usually the blocker
         Mode: Directive (clear situation, data available)
         Confidence: Level 2 (strong inference, numbers support it)
Stage 7: Length = 3-4 sentences (match thread energy, analytical)
Stage 8: Domain = SaaS (loads domain-brain)
         Thread gap: nobody ran the actual math on churn vs acquisition
Stage 9: Quality gate pass
Stage 10: Output
```

### Output
```
Run the math on your churn. At 8% monthly, you're losing ~24 customers 
per year if you have 300, which means you need 24 new customers just to 
stay flat. Your growth channels aren't failing: they're being eaten by 
the leak. Fix retention before you spend another hour on acquisition. 
One exit survey question to every churned customer will tell you more 
than six months of marketing experiments.
```

---

## Example 3: Emotional Post (Gate Triggered)

### Input
```
/reddit

r/startups

Title: I think I'm done.

Body: 2 years. $200K of my savings. My wife barely talks to me anymore. 
The product works, customers like it, but I can't get past $1K MRR. 
I'm 38 and I feel like I've wasted the best years of my life on this. 
Every morning I wake up and dread opening my laptop. I don't even know 
why I'm posting this. Maybe just to say it out loud to someone.
```

### Pipeline Trace
```
Stage 1: Format 1 (thread only), no operator instructions
Stage 2: Grief Poster (4/5 signals) + Burnout Denier (3/5)
         Primary: Grief Poster
Stage 3: Intermediate-Advanced (built a product, has metrics)
         Emotion: Defeated (hopelessness, dread, "wasted")
         Personality: S (Steady, processing out loud)
Stage 4: GATE 1 TRIGGERED — Emotional Crisis
         Not safety-critical (no self-harm signals)
         Action: Address emotional content FIRST
Stage 5: Skip
Stage 6: Skip (emotional post, not strategic)
Stage 7: Length = 2-3 sentences (short for defeated emotional state)
Stage 8: Validate first, substance second
Stage 9: Quality gate — extra check on empathy authenticity
Stage 10: Output
```

### Output
```
The fact that you built something customers actually like after 2 years 
puts you ahead of 90% of founders who never shipped. That's not wasted 
time, that's proof you can build. The dread and the marriage strain are 
telling you something your spreadsheet can't: it might be time to take 
what you've learned and apply it somewhere the economics work, even if 
that's a job for a while. There's no shame in a strategic retreat.
```

---

## Example 4: Technical Question (Direct Answer)

### Input
```
/reddit max 2 sentences

r/webdev

Title: Is Next.js overkill for a simple blog?

Body: I just want a blog with maybe 20 posts. No e-commerce, no user accounts, 
just articles. Everyone keeps recommending Next.js but it feels like bringing a 
tank to a knife fight.
```

### Pipeline Trace
```
Stage 1: Format 1, operator instruction: max 2 sentences
Stage 2: Analysis Paralysis (2/5), not strong match; Simple question
Stage 3: Intermediate (knows Next.js by name, "overkill" = understands scale)
         Emotion: Confused
Stage 4: No gates triggered
Stage 5: Skip
Stage 6: Skip (simple question)
Stage 7: Length = 2 sentences (operator constraint)
Stage 8: Domain = Web Dev (loads domain-brain)
Stage 9: Quality gate pass
Stage 10: Output
```

### Output
```
Your instinct is right. For 20 static posts with no dynamic features, 
Astro or even plain HTML with a static site generator will ship faster 
and cost you nothing to host.
```

---

## Example 5: Wrong Premise (Gate 5)

### Input
```
/reddit

r/SEO

Title: Why SEO is dead in 2026

Body: With AI overviews taking all the clicks, there's literally no point 
in doing SEO anymore. I've seen my traffic drop 40% in the last year. 
Every query just shows an AI answer now. Companies should just invest 
everything in paid ads and social media instead.
```

### Pipeline Trace
```
Stage 1: Format 1 (thread only)
Stage 2: Rage Poster (3/5) + Confident Incompetent (3/5)
         Primary: Confident Incompetent (wrong conclusion from real data)
Stage 3: Intermediate (specific metrics, knows terminology)
         Emotion: Frustrated
         Personality: D (Dominant, assertive conclusion)
Stage 4: GATE 5 TRIGGERED — Wrong Premise
         Kernel of truth: AI overviews DO change CTR
         Wrong part: "SEO is dead" is the wrong conclusion
Stage 5: Would verify traffic claims, but no specific URL given
Stage 6: Loads cognitive-engine
         Mode: Validate-then-Challenge (real frustration, wrong conclusion)
         Confidence: Level 2 (SEO is domain expertise)
Stage 7: Length = 3-4 sentences (need to validate AND correct)
Stage 8: Domain = SEO (loads domain-brain)
Stage 9: Quality gate pass
Stage 10: Output
```

### Output
```
The 40% drop is real and a lot of people are seeing it, so you're not 
wrong about the trend. But "SEO is dead" is the wrong conclusion from 
that data. What's actually dead is ranking for informational queries 
where an AI overview can fully answer the question. Transactional and 
commercial queries still drive clicks because people don't buy from AI 
summaries, they buy from pages they trust. The play now is shifting your 
content strategy toward those high-intent keywords instead of 
abandoning the channel entirely.
```

---

## Notes on Examples

- Pipeline traces are illustrative. The actual AI doesn't output the trace; it processes internally.
- Real responses may vary: the pipeline is deterministic in structure but not in output.
- Examples show the system working correctly. For examples of what goes wrong without the pipeline, see [ARCHITECTURE.md](../ARCHITECTURE.md#anti-patterns-the-architecture-prevents).
