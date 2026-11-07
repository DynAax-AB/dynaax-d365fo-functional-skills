# Contributing

Thanks for helping. These skills are only useful if they're right, so every
change is reviewed by someone who works with F&O every day.

## Ways to help

- **Report a wrong answer.** Open an issue with the question you asked, the
  answer you got, and what the right answer is. Remove customer names and
  personal data first.
- **Improve a skill.** Fix a menu path, add a common cause, add a test question.
- **Add a new skill.** Open an issue first to agree the scope, so two people
  don't write the same one.

## Writing a skill

1. Copy `docs/skill-template.md` to `skills/<your-skill-name>/SKILL.md`. The
   folder name and the `name:` field must match: lowercase letters, numbers and
   hyphens.
2. Put longer lists and tables in `skills/<your-skill-name>/references/`, and
   point to them from `SKILL.md`. Keep `SKILL.md` under 500 lines.
3. Add `skills/<your-skill-name>/test-questions.md` with 3 to 5 questions and
   the points a good answer must cover. Include one question where the right
   answer is "hand this over to a person".
4. Keep the status `draft: Nurlin to review` until the review is done.

### Rules

- **Your own words.** Don't copy text from Microsoft Learn, blogs or training
  material. Link to the source instead.
- **Real menu paths.** Check each menu path in an environment and say which
  version you checked in `checked-against`. If you're not sure about something,
  leave a comment in the file: `<!-- REVIEW: what needs checking -->`.
- **No customer data.** No customer names, real account numbers, screenshots
  with personal data or anything under NDA.
- **Read-only advice.** Skills explain and point to where to look. They never
  tell users to change data in the database or skip validation, and they always
  say to test setup changes in a sandbox first.
- **Plain language.** Write for a key user, not a developer. Short sentences.
  Explain F&O terms the first time you use them.
- **No product promotion.** No links to paid products or services.

## Check your changes

With Python 3 installed:

```bash
python3 tests/check_skills.py
```

This checks the frontmatter, the required sections, the test questions and that
links point to Microsoft Learn over https. To also check that every link still
opens:

```bash
python3 tests/check_skills.py --online
```

The same checks run on every pull request.

## Review

The maintainer reviews every pull request for accuracy and may test the
questions in a sandbox. When a skill has been checked, its status changes to
`reviewed` and `checked-against` names the F&O version.
