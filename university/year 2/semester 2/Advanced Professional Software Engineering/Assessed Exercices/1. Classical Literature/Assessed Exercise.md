#apse 
# Part A: Reading Notes

## [Naur’s “Programming as Theory Building”](https://pages.cs.wisc.edu/~remzi/Naur.pdf)

I found this text quite interesting, though overly wordy, like the writer is trying his best to meet a word count.

The main idea `knowledge can be determined by a person's ability to complete a task effectively, provide justification, answer questions, and explain issues` is very true to me. I've seen this proven repeatedly. I'd say I value actual knowledge of implementation and how things will work in the real world way more than theoretical knowledge.

When Naur goes on to discuss `The Theory to Be Built by the Programmer`, I agree even more. For a developer to code effectively, they need to understand:

1. How the solution relates to the real-world problem.
2. Why each part of the program is designed the way it is.
3. How to justify design decisions and respond to criticism.

In my experience, this is massively important. While my company doesn't emphasise it as much, I've noticed that in tons of others in the apprenticeship programs, the focus leans more toward discussing and understanding projects rather than actual implementation. 
## [Heddleston’s “The Null Process”](https://www.kateheddleston.com/blog/the-null-process)

Quite a dry one overall but it does bring up some compelling points. The core argument is about  removing the stigma around processes, which I'll admit can be a big problem especially at fast moving start ups, some argue that addressing this directly could lead to massive improvements, while others say it may be diminishing to productivity.

I've been in situations like those described in the text - looking blankly at an issue unsure whether I've done this correctly or to a standard that is expected. Heddleston suggests this should be a case in which we would set up a new process, but this is where my experience differs: when I asked, I was told to observe how others tackled similar issues. This highlights a large omission from the article, **context and pre-requisites matter**. If the necessary information is there and openly available, people should be able to figure out what's needed without relying solely on a formalised processes.

Automation is another area where I completely agree. Standardising workflows through automation reduces human error and streamlines tasks, can't have human error if the work is done by a computer. After weeks of struggling with developers mismanaging deployments via Google Play Console, I switched to an automated deployment pipeline, which made things significantly easier.

This kind of process improvement is exactly what I believe companies should prioritise and I'm glad we agree on this main point, that our focus should be on enhancing efficiency, not creating bureaucratic glue traps.

## [Hamilton’s “What the Errors Tell Us”](http://www.htius.com/Articles/what-the-errors-tell-us.pdf)

This was really cool, I couldn't really relate 100% relate to the high stakes of having human life's on the line like the Apollo mission but I can still see some similarities when it comes to the core principles brought up by Hamilton, testing, fault tolerance, automation and rigorous validation.

Just like the engineers on the Apollo project simulated the hardware, we simulate the program flow through unit and integration tests. For Apollo, these simulations were designed to ensure the software could handle edge cases without jeopardising the mission. For me, the goal is much simpler, it's about flagging when developers accidentally break unrelated parts of the code.

What really stands out to me is how, despite the difference in context, both the **Apollo engineers** and **modern software teams** emphasise identifying potential failure points before they fail. Testing serves as a safety net for both, ensuring that no matter how small the issue, it's caught early and addressed before it can lead to major consequences.

## [Raymond’s “The Cathedral and the Bazaar”](http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/)

This text is centred around discussing why open sourced software is successful as it is and how that relates to the older philosophies of software engineering, these are split into two categories:

- **The Cathedral**, The traditional development cycle, think of it like an exclusive, tightly controlled project. A small team of industry experts works in isolation, carefully creating and refining everything before releasing a polished product. This is how traditional software companies operate, long development cycles and big releases.

- **The Bazaar**, This is the complete complete opposite, instead of it being exclusive, it's an open discussion where anyone can contribute, suggest changes, and improve the software continuously. Updates happen frequently, and the project evolves dynamically with community input. This is how Linux and most open-source projects thrive.

# Part B. A Null Process?

#### [Heddleston's "The Null Process"](https://www.kateheddleston.com/blog/the-null-process)

# Intro

A team's efficiency is largely determined by its processes, and one of the key ideas in Heddleston's "The Null Process" is the potential consequences of **null** processes (situations where a process is either missing or poorly explained). While the article might come across as dry overall, it brings up really interesting points, particularly around the stigma associated with processes. As Heddleston states, "Our fear of 'unnecessary process' has created workplaces with something worse than bad process: no process." This stigma is seen as a massive issue, especially in fast-moving startups, where some argue that addressing it directly could lead to huge improvements. In contrast, others claim it might actually diminish productivity.

# Trust in the Individual

In my experience, I've encountered many situations similar to those described in Heddleston's text. Looking blankly at a screen, unsure if I'd approached a problem correctly and met the expectations set out. According to Heddleston, this is a scenario where a new process should be implemented to help guide decision-making. However, this is where I diverge from this text. When I faced a similar situation and asked for guidance, I was instead told to observe how others had handled similar issues. 

This experience highlights one of the biggest things Heddleston's missed: **context and pre-requisites matter**. If the necessary information is out there and is well communicated, individuals should be able to decide the appropriate course of action without relying on a formalised process. In such cases, fostering an environment where resources and knowledge are widely available can often be more beneficial than the imposition of rigid processes. This not only allows an individual to work independently without help from other members in their team it also gives them a better understanding of what they're doing as opposed to following a set checklist.

# Processes at Different Scales

This hesitance to process might be quite telling of my experience, all I've had experience with is in a smaller company. That's another thing that isn't mentioned in Heddleston's text, the importance of processes in a team massively depends on a company's scale and speed, like I mentioned before. Startups, especially in the early stages, tend to stray away from the traditional process approach and stick to a more "if it works, it works" mindset, this approach can help keep them stay agile and quick to adapt. However, as they scale, they normally need to introduce more structured processes to accommodate a growing team with diverse experiences and working styles.

At larger scales, I find myself seeing it more from Heddleston's perspective. In the past few months, there's been quite massive change and growth at my company. This has been really evident in the amount of processes being put in place. While I would argue that some of them are unnecessary, there is one that I strongly believe was needed: the process for rebasing customer websites onto later versions. Previously, this was a case of rebasing, testing, and pushing. This was an insane approach for such a critical and complex task, yet it worked and worked well, it was only 12 or so developers doing it and they all had a common understanding of how it's done. However, as we expanded and new developers took on this responsibility, differing interpretations of the workflow led to errors. Implementing a structured process helped mitigate these inconsistencies and ensured a smoother transition for customer sites.

When teams must coordinate between 20 to 30 employees, I've found the need for well-defined processes becomes increasingly potent. Startups that don't adapt to the more structured approach may find themselves struggling with inconsistency and preventable mistakes. The key challenge here is in identifying the right time to formalise the company and swap to a more structured system.

# Automation in place of Processes

Heddleston describes how automation can reduce human error although I don't think she really emphasised how this can actually remove the need for most processes. I'm of the strong belief that anything that can be laid out as a step-by-step process can and should be automated. I've seen situations reinforcing this time and time again.

A prime example comes from my experience working on an app with a small team - just me and one other developer, I handled the infrastructure, including deployment and CI/CD, while my colleague focused on development however there was a large issue with this division of work, the developer I was working with had no understanding of the deployment process.

Initially, I saw this as an opportunity to introduce a structured process, but I very quickly realised the mistake I made. Despite the process being clear and all steps being listed, almost every time we attempted to deploy there would be issues, not issues due to the process being unclear or lacking steps. It was due to inevitable human error, which can't be blamed on the developer it should just be expected. This created massive slowdowns in deploys while I wasn't there.

Rather then repeatedly attempting to refine the process to no improvement, we opted to implement a CI/CD pipeline to handle this automatically, While this reduced my colleague's direct knowledge of the process, it was a worthwhile trade-off. He saw no real benefit in following a manual checklist when automation could handle the task more efficiently and consistently. This experience reinforced my belief that process-heavy tasks should be streamlined through automation whenever possible. As Heddleston states, "Create internal tools that automate and minimise process so that computers are in charge of remembering the steps to complete a task instead of humans."

# Conclusion

In the end, the key takeaway for me is that processes are important but must evolve based on the needs of the team and the company. There will be times where a clear, formalised process is needed to avoid devolving into chaos. But there will also be moments where adaptability, collaboration, and trust will drive better results. 

The challenge, therefore, is finding the right balance between structure and freedom (between process and autonomy) so that efficiency is maximised without stifling creativity or growth. By recognising when processes should be implemented, refined, or even replaced with automation, companies can foster a work environment that promotes both productivity and innovation.
