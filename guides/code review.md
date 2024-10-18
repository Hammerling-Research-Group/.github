# Getting Started with Code Review
### Hammerling Research Group, Colorado School of Mines

## Introductory Remarks

This quick start guide is intended to help team members at HRG conduct rigorous and productive code reviews, ensuring that every contribution to the production codebase meets our standards for quality, clarity, and correctness.

Code review is an essential part of open development, and in HRG, we aim to foster a culture of constructive, collaborative feedback. Reviewing code not only helps to catch bugs but also improves code readability, ensures adherence to best practices, and enhances the overall skillset of the team.

*The bottom line:*

  - *Collaborate, don't critique*: The goal of code review is to help your fellow team members write better code, *not* to criticize their work.
  
  - *Prioritize correctness, clarity, and style*: Focus on ensuring that the code does what it's supposed to, is easy to understand, and follows HRG's established standards.
  
  - *Learn as you review*: Code reviews are an opportunity to learn about different parts of the codebase, new techniques, or unfamiliar tools and methods.

Let's walk through some best practices and other tips for engaging in helpful and rigorous code review.

## Mechanics of Conducting a Review on GitHub

Almost always, members will be invited to be a reviewer on a piece of code. Often this person is either the admin on the repo and/or the codebase maintainer. Sometimes for more complex changes, a second review will be added for extra care and credibility. 

Once added as a reviewer, you will see a list of all files changed, as well as line-by-line locations of all changes made. If the suggested changes are to existing code (and not new code), then you will see a side-by-side comparison of the changes being suggested. 

You can navigate to and through individual files, and click the plus sign on any line that requires attention. 

Once there, you can offer comments (markdown formatting is supported), and/or "start a review." The latter is a formal way to keep track of all comments and suggested changes or revisions to the code under review. 

Once finished with the review, you can either approve the pull request or not. If approved, you can merge to `main` and be done. If not, then it gets sent back to the developer who must address or at least respond to all suggestions, revisions, and corrections. In some cases, a suggested change could be caused by confusion from the reviwer. These points of confusion must be hashed out in the discussion and then resolved. 

Once resolved and changes made, the reviewer goes back into the code, reviews again as before, and has the option to approve or reject. This cycle continues until the suggested code changes are approved and merged to `main`. 

## Best Practices for Open Code Reviews

Now, with the mechanics out of the way, let's cover some of the foundational and widely recognized best practices for conducting code review in an open, collaborative development context. 

  - *Review promptly*. Timely feedback is critical. Delayed reviews slow down the entire team and block feature development.
  
  - *Balance detail with speed:* While it's important to provide thorough feedback, avoid spending too much time on trivial issues, especially when it holds up progress. Flagging those issues without blocking approval can sometimes be more productive.
  
  - *Avoid nitpicking*: Don't overwhelm the author with minor stylistic suggestions. If the code works and follows general guidelines, try to focus on higher-level improvements.
  
  - *Be open to learning*: Code reviews are two-way learning processes. If the code introduces a new technique or approach you're unfamiliar with, *ask questions*. This can help you grow while also giving the author/developer a chance to explain their thought process. 
  
## Diving Deeper

Now, let's pull some of these best practices and ideas apart a bit more, and introduce some new ones too. *This list of ideas is by no means exhaustive*. Rather, all of these ideas are merely suggestions for conducting a useful code review for a common development goal. Members are welcome to follows some or all of these pointers. Likely newer team members or members who are new to this type of development will find this more useful than others. 

Ultimately, the goal with this guide is to provide a starting place for HRG members to think about and implement code reviews well, and also to ensure everyone has at least the same initial footing.  

  - Begin by understanding the context
  
      - Before jumping into the code, read through the pull request (PR) description carefully. 
      
      - Make sure you understand the problem the author/developer is trying to solve first, and then how their changes are supposed to address it. If the PR is related to a specific issue or bug report, it is a good idea to review that context as well to understand the broader implications.

  - Review code correctness
  
      - Though seemingly obvious, ensure that the code does what it claims to do. This is the highest priority in any code review.
      
      - Check for edge cases and see if the PR addresses unusual inputs or scenarios, or whether these expectations are assumed or clearly stated. Is the code likely to break or behave unexpectedly in specific conditions?
      
      - Review any test cases. Does the testing code cover a broad enough range of scenarios? Could more tests be added to catch potential future issues? Code coverage reports will help with this. 

  - Assess code readability and clarity
  
      - Code readability is arguably as important as correctness. Can you (or any reasonable human) easily follow what the code is doing? If not, make suggestions to simplify or clarify the logic.
      
      - Are variable names, function names, comments, etc. descriptive and meaningful? Encourage the use of clear, self-explanatory names and inline documentation where necessary.
      
      - Is the code modular? Well-structured code typically separates concerns and avoids duplication. Highlight any areas where large blocks of code could be split into smaller, more focused functions and/or where redundancies are detected.

  - Ensure adherence to style guidelines
  
      - Consistent style across the codebase is essential for long-term maintainability. For example, does the code follow HRG's established linting and formatting rules?
      
      - Consider suggesting changes where style diverges from HRG standards.
      
      - As HRG uses automated linters and testing workflows, ensure these tools have been run *successfully* on the PR. Typically, code will get to the human review stage once successfully passed. But there could be cases where the code was not successful. Check, assess and respond to these instances accordingly. 

  - Check performance and efficiency
  
      - Does the new code introduce performance bottlenecks? For example, be on the look out for inefficient algorithms or unnecessary computational overhead (e.g., excess looping, excess object creation, etc.).
      
      - When possible, encourage optimization, but remind authors/developers that readability and clarity should *not* be sacrificed for marginal performance gains. In more complex cases, you may even consider suggesting the author/developer construct a benchmarking experiment to demonstrate the tradeoffs in efficiency vs. readability, and so on. Use good judgement here, but don't be afraid to suggest a little extra work *if it would benefit the development and production code*
      
      - Ultimately, if performance improvements are needed, suggest alternatives and provide reasoning.

  - Encourage minimal, focused changes
  
      - It is the responsibility of the author/developer to ensure the PR is small and focused on (ideally) one feature or fix. If the changes are too broad or involve multiple unrelated changes, suggest splitting the PR into more manageable parts.
      
      - Large PRs are more challenging to review thoroughly and introduce a higher risk of errors. Yet, if needed for the specific application, context, or fix, consider workshopping alternatives with the author/developer or inviting additional reviewers to support. 

  - Run the code locally, when possible
  
      - If time allows, check out the PR branch locally and run the code to verify that it functions as expected and as presented. This can be especially important for larger or more complex changes.
      
      - If you encounter issues when running the code, let the author know by providing specific, actionable feedback, which may require the author/developer going back to revise and re-initiate the PR when the code is in better shape. 

  - Consider future maintainability
  
      - Look for signs that the code will be easy to maintain in the future. This includes well-documented functions, clean abstractions, and modularity.
      
      - Ask whether the given change introduces technical debt. That is, "the implied cost of future reworking because a solution prioritizes expedience over long-term design" (<https://en.wikipedia.org/wiki/Technical_debt>). If so, suggest ways to mitigate it before merging the PR.
      
      - If the code introduces new dependencies, ensure they are necessary and justified.

  - Use respectful and constructive language
  
      - Avoid using confrontational language. Phrase suggestions in a collaborative way. For example, instead of saying, "This is wrong," try instead something like, "Have you considered doing it this way?" or "This might be clearer if...", and so on.
      
      - *Acknowledge good work*. Pointing out what was done well is equally important as highlighting areas for improvement. And unfortunately, praise in this context is often overlooked, forgotten, or at best, assumed. But don't make these assumptions. People like to hear that they're doing good work, especially when they are in fact doing good work. So, make an effort to point out cool ideas, innovative thinking, or creativity. It will go a long way toward strengthening the HRG community and also will likely make the author/developer more receptive to your suggestions. 

  - Communicate clearly on follow-ups
  
      - If the author needs to make changes based on your review, explain what you expect in a follow-up or comment. Offer examples or detailed explanations, especially if your suggestions are complex.
      
      - When additional changes are made by the author/developer, re-review the PR thoroughly, ensuring new issues are not introduced and also that formerly cited issues have been addressed.
