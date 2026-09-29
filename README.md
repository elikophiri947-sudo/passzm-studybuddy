# PassZM StudyBuddy

An AI tutor for Zambian Grade 1–12 learners, built to explain ECZ past-paper questions step by step using [PassZM](https://passzm.infinityfreeapp.com)'s own exam papers and study notes.

> **Status: proposal / early planning.** This repository describes the planned project and its architecture. The implementation roadmap below shows what will be built and in what order.

---

## The problem

PassZM provides free past exam papers and study notes aligned to the ECZ national curriculum for Zambian Grade 1–12 learners. But a PDF cannot tell a learner *why* their answer was wrong. Many learners have no access to a tutor, and many are on limited data bundles and low-cost phones, so heavy or always-online tools are out of reach.

## The solution

**StudyBuddy** is an AI tutor built into PassZM that answers from the platform's own curriculum-aligned content rather than from the open internet.

### Planned features

1. **Past-paper explainer.** The learner selects a paper and a question and receives a step-by-step explanation pitched at their grade level.
2. **Practice question generator.** Produces new questions in the style of ECZ papers for a chosen subject and topic, with marking guidance.
3. **Weak-topic tracker.** Records which topics a learner keeps getting wrong and suggests what to revise next.
4. **Low-bandwidth design.** Short text responses, a lightweight mobile-friendly interface and cached content so it works on cheap phones and small data bundles.

## Planned architecture

```
Learner (mobile browser)
        |
        v
  Lightweight web UI  <---->  PassZM (WordPress) via plugin / embedded widget
        |
        v
  FastAPI backend (Python)
        |
        +--> Retrieval layer: vector index of PassZM papers and notes
        |
        +--> Open-source LLM (self-hosted, prompted with retrieved context)
        |
        +--> Progress store: per-learner topic performance
```

- **Retrieval-augmented generation (RAG):** PassZM papers and notes are split into chunks and embedded into a vector index. For each question the system retrieves the most relevant syllabus content and gives it to the model, which keeps answers curriculum-aligned and reduces made-up answers.
- **Open-source model:** A small open-source language model, prompted (and fine-tuned if results justify it) for step-by-step explanations at school level. Self-hosting keeps the system independent of paid external APIs.
- **Backend:** Python with FastAPI serving the model and retrieval layer.
- **Front end:** A simple, responsive web interface that can be embedded in the existing WordPress site.

## Evaluation plan

- Compare StudyBuddy's answers against official ECZ marking schemes on a sample of past-paper questions and record accuracy by subject and grade.
- Review a sample of explanations for clarity and grade-appropriate language.
- Run a small pilot with learners and collect feedback on usefulness and data use.

## Roadmap

- [ ] Collect and clean PassZM papers and notes into a structured dataset (subject, grade, year, topic)
- [ ] Build the retrieval index and test search quality
- [ ] Prototype the question-explainer with an open-source model
- [ ] Build the FastAPI backend and a minimal web UI
- [ ] Add the practice question generator
- [ ] Add the weak-topic tracker
- [ ] Integrate with the PassZM WordPress site
- [ ] Evaluate against marking schemes and run a learner pilot

## Sustainable Development Goals

- **SDG 4: Quality Education.** Free, curriculum-aligned help for learners who cannot otherwise get tutoring.
- **SDG 10: Reduced Inequalities.** Narrows the gap between learners with access to tutors and those without, including rural and low-income learners.
- **SDG 9: Industry, Innovation and Infrastructure.** Builds local AI capability using open-source models and low-bandwidth design.

## About

Created by **Eliko Phiri**, University of Zambia student and founder of [PassZM](https://passzm.infinityfreeapp.com), a free educational platform for Zambian learners.

## License

To be decided. Note that the past papers and notes themselves remain subject to their original copyright and are not part of this repository.
