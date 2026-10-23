# Reflection

Student: Aman Priyansh (PES1UG24AM030)

Note: the lab handout PDF I was given does not list the reflection questions, so these are the usual four themes from the learning outcomes. Replace the headings with the exact wording from your teacher if it differs.

## 1. Which tool reported the most issues, and which fixes mattered most?

Pylint reported the most (26 messages), but most were naming and docstring messages that are about readability. Bandit reported only 4, yet the High one (os.system with a string built from input) was the most serious because it allows command injection. So the count of issues and the importance of issues are not the same thing.

## 2. Did any tool give a false positive, or did a fix change behaviour?

The hardcoded password warning (B105, Low severity, Medium confidence) is close to a false positive: the value was a demo string and was never used, so nothing could leak. I still removed it because secrets in source code are a bad habit. No fix changed behaviour: the program printed exactly the same output before and after.

## 3. How do the three tools differ?

Pylint looks at code quality and likely bugs (mutable default argument, unused argument). Flake8 only checks style against PEP 8 (spacing, blank lines, line length). Bandit only looks for security problems (shell calls, unsafe XML parsing, hardcoded secrets). They overlap very little, so using all three gives better coverage than any one alone.

## 4. How does static analysis help code quality and maintainability?

It finds problems without running the code, so bugs like the mutable default argument are caught before they cause a wrong result. It also keeps a team's code in one consistent style, which makes it easier to read. It cannot find logic mistakes in the billing slabs, so tests are still needed alongside it.
