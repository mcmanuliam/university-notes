#apse 
# Introduction

**Creating a good product**, was the only real goal I set for us when starting this project. However, looking back, I can't help but feel that we fell a bit short of that goal. I had really high expectations going into the project, and what we accomplished, while really cool, felt quite underwhelming, I know we could have done more, especially given the diverse skill sets we had within the team. 

With that in mind, this essay serves as a retrospective on our project, highlighting the areas where we fell short and the lessons we can take forward in the future.
# **Contrasts** And **Similarities** in the Engineering Process

## Us vs. Stakeholder Observations

As part of our group project, we acted as stakeholders in another team's project, which offered valuable insights into their engineering processes.

One of the main differences was the other teams work distribution. They used more of a role based strategy with dedicated developers for `database`, `frontend`, and `backend`. This ensured high quality work in every area but required constant back and forth communication. In contrast, our team split work more evenly, regardless of expertise, which allowed us to work independently but resulted in inconsistencies, especially in the `frontend`.

Another difference was how retrospectives were handled. Both teams used the 'Start, Stop, Continue' method, but the other team voted on the most important issues to discuss. While intended to save time and effort, I found this approach really harmful. Retrospectives should allow time to reflect deeply on all feedback, and in prioritising only the top-voted points, they risked overlooking less popular concerns.

## Us vs. The Industry

Having been in the industry for over a year now, I've noticed a few key differences between my experience in the workplace and the group project. 

A massive difference is the strong focus on strict development practices, such as unit testing, `linting`, `CI/CD`, and harsh code reviews. When I introduced these to my team, they found them frustrating, especially quick and simple issues like a missing trailing comma. While I viewed these as very helpful some viewed them as unnecessary hurdles.

Another difference is the lack of formal retrospectives in my work. While retrospectives are common across the industry, my company prefers a more informal approach. Issues are raised as they are found, and reflection happens passively. This is completely different from the retrospectives in our project. I believe that shortening these to simple brief actionable discussions could massively improve our efficiency.

The most obvious difference, is again work distribution. In the workplace, we work as T-shaped developers, adapting to all different tasks. This flexibility prevents the bottlenecks we faced during the project, where the specialised skill set distribution led to inefficiencies.

# The **Good**, the **Bad** and the **Ugly** of Our Software Engineering Processes

Looking back, there were definitely positive aspects to our processes, but equally there were tons of areas to improve:
## The Good

- [**Code Safety**](https://stgit.dcs.gla.ac.uk/apse/platform/-/tree/main/frontend?ref_type=heads): We had really good code safety across the `frontend`, especially due to testing, linting, and CI/CD. This made it much harder for developers to push broken code, ensuring that our `frontend` remained stable and clean.

- [**Backend Quality**](https://stgit.dcs.gla.ac.uk/apse/platform/-/tree/main/backend?ref_type=heads): Given that our team was more `backend` developers, we had a high level of code quality on the `backend`.
## The Bad

- **[Documentation Issues](https://stgit.dcs.gla.ac.uk/apse/platform/-/wikis/home)**: One of our biggest weaknesses was the lack of understanding regarding documentation's role. This often led to overly detailed documentation on irrelevant subjects, causing confusion and wasting time. You can see this in a few of the docs on the sidebar and especially if you start looking at the `README.md`.

- [**Work Distribution Problems**](https://stgit.dcs.gla.ac.uk/apse/platform/-/issues/?sort=updated_desc&state=all&first_page_size=20): As mentioned before, work distribution was a major issue. We faced a bunch of different issues with issues being developed over the two sprints and hitting blockers that wouldn't move for days.

- **Lack of Support for Less Experienced Developers**: There wasn't much help out there supporting less experienced team members. This wasn't discussed during the project but if improved could've easily fixed the workload issue.
## The Ugly

- **Inexperienced Reviews**: There were instances where less experienced developers were tasked with reviewing code far outside their comfort zone. This resulted in bad reviews, missed errors, and memory leaks across the `frontend`.

- **[Commit Conventions](https://stgit.dcs.gla.ac.uk/apse/platform/-/commits/main?ref_type=HEADS)**: Another big issue was our lack of clean commit conventions. We ran into a lot of problems with commits being merged without squashing, leading to a horrible main branch filled with `feat`, `fix`, `fix`, `fix`. This not only cluttered the commit history but also made it way harder to track and understand the changes being made over time.

# **Improving** Our Software Engineering Process, in Retrospect

## Lack of Experience * Lack of Support

One of the most pressing issues was the lack of support for less experienced developers. This wasn't necessarily a matter of individual capabilities, but rather a lack of structured assistance for those who needed it. In a team with varying levels of expertise, it was easy for less experienced developers to struggle without clear guidance.

Moving forward, setting up more formal channels for collaboration, and problem-solving would be crucial. Whether through dedicated "Developer Learning" channels, pair programming, or regular check-ins, ensuring that all team members feel a bit more supported.

## The Dreaded `feat`, `fix`, `fix` Master

[Our commit history](https://stgit.dcs.gla.ac.uk/apse/platform/-/commits/main?ref_type=HEADS) was a mess, no sugarcoating it. We often merged commits without squashing, and many commit messages were a bit vague, making it difficult to trace the history. 

To improve this, we should have enforced a stricter commit convention and made commit squashing a standard practice. This would not only clarify the version control history but also aid in debugging and collaboration.

## Work Distribution

[Work distribution](https://stgit.dcs.gla.ac.uk/apse/platform/-/issues/?sort=updated_desc&state=all&first_page_size=20) was easily the most significant challenge in our project. As mentioned earlier, the team had a wide range of skills, but we struggled with assigning work, especially when it came to `frontend` tasks.

Moving forward, it would be beneficial to determine the team's skills and assign tasks based on that, also ensuring that everyone has lots of support and can contribute across different aspects of the project would help encourage more balanced workloads.

# Handling the Unexpected… the So-called **Curveball**

When the curveball hit, we faced a massive issue, it became clear that our workload distribution wasn't ideal, everyone already had their hands full, and those who could take it on didn't have enough familiarity with the required technologies. As a result, I ended up taking it on myself, which was tough given my other work at the time.

In hindsight, it would have been better to split the workload between the `frontend` and `backend` teams. Unfortunately, some situations are outside our control, and we must adapt as best as we can.
# Conclusion

Reflecting on this project, there were many lessons learned. Our team's engineering process had both its strengths and its weaknesses. Improving work distribution, supporting less experienced developers, and maintaining clean-commit practices will make our future projects more efficient and successful. By incorporating these lessons and embracing industry best practices, we can elevate the quality of our work and achieve better results in the future.
