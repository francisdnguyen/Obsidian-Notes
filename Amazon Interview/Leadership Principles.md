- Used every day, whether its for discussing ideas for new projects or deciding on the best way to solve a problem

# Customer Obsession

## Definition
- Leaders start with the customer and work backwards.
- They work hard to earn and keep customer trust.
- They pay attention to competitors, but they obsess over customers.

## Key ideas
- **Everything starts with the customer** and works backwards from there.
- **Working backwards before writing code**
  - Write a press release first to confirm the product would actually matter to customers.
  - Write an FAQ to vet everything in advance:
    - What problem are we solving?
    - What will customers care about most?
    - What will they love most?
    - What would disappoint them if we launched with this feature set?
- **Economics and sustainability are part of customer obsession**: exciting customers with something you can't sustain doesn't serve them long-term.
- **Competitors matter, but customers come first**
  - Be aware of what competitors build. If customers love it, learn from it and use it to improve our own customer experience.
  - Spend most of your time on what customers care about most.
- **It's everyone's job**: every employee has the freedom and the expectation to figure out what customers want and get better for them every day.
- **Examples at Amazon**
  - **Customer reviews**: added reviews to book pages even though publishers worried about negative ones, because honest reviews help customers decide.
  - **AWS during the pandemic**: proactively helped customers cut costs instead of maximizing revenue, so they could reinvest and survive a tough economy.
  - **Kozmo (counterexample)**: one-hour delivery that customers loved, but it was uneconomical and gone within a couple of years.

## My example: Feather Software client work
- **Situation**: [client, what they asked you to build]
- **Action**
  - [How you figured out what they actually needed vs. what they asked for]
  - [Where you pushed back on or refined the request]
  - [What you built as a result]
- **Result**: [outcome for the client: time saved, adoption, repeat business, referral]
- **Customer Obsession angle**: worked backwards from the client's real need instead of building exactly what was first requested.
# Ownership

## Definition
- Leaders are owners: they think long term and don't trade long-term value for short-term results.
- They act on behalf of the whole company, not just their team.
- They never say "that's not my job."

## Key ideas
- **A mindset, not just a behavior**: the most attitudinal of all the leadership principles.
- **Reliability**: when you tell your team you've got something, you've got it. Nobody should have to keep reminding you.
- **Think like it's your own money**: great owners ask what they'd do if it were their personal money on the line.
- **Renters vs. owners**: a renter might nail a Christmas tree into the wood floor; an owner never would. Treat the business like you own it.
- **Care beyond your role and pay**: counterexample is a young store employee who wouldn't suggest revenue ideas because they didn't get a commission and it wasn't "their area." That's not ownership.
- **Make sure problems are owned**
  - If an issue has no clear owner, find the owner. Don't assume someone else has it.
  - If work looks half-finished or the handoff is unclear, make sure the handoff happens, or take care of it yourself.
  - Every problem should have a path to resolution, and owners drive it themselves when needed.
- **Don't punt hard problems**: pull the right people together to find the best solution for customers.
- **Whole-company, long-term view**: think about issues from the entire company's perspective, over the long run.

## My example: UMD research lab image pipeline
- **Situation**: the lab produced 200–300 test images per day, and they needed to be sorted by honeycomb model, tension strength, and date.
- **Action**
  - Built an automated Python/PowerShell pipeline that read EXIF metadata and sorted images into model, then tension, then date folders.
  - Ran it on scheduled polling (Task Scheduler) so it kept up with new images without anyone triggering it.
  - Read failures were caught, logged, and moved to a separate folder, so no image was silently lost.
- **Result**: processed 1,200+ images per week and saved about 8 hours per week of manual work.
- **Ownership angle**: built it to keep running after I was done (long-term over a quick fix) and handled failure cases so the lab wasn't left with a fragile tool.

# Invent and Simplify

## Definition
- Leaders expect and require innovation and invention from their teams, and always look for ways to simplify.
- They are externally aware and take good ideas from anywhere, not just ideas invented in-house.
- When doing new things, they accept they may be misunderstood for long periods of time.

## Key ideas
- **Keep inventing after the first big idea**
  - Many companies succeed on one innovative idea, then only make small tweaks to it.
  - With technology changing this fast, staying successful means constantly inventing and reinventing.
- **Two kinds of invention**
  - **Whole-cloth invention**: building something entirely new.
  - **Reinvention**: completely rethinking an existing business and its customer experience.
- **Simplifying assumptions unlock success**: the right simple idea can turn a failing approach into a working one, even if it looks obvious in hindsight.
- **Customers decide the debate**: when there's internal resistance, side with what's better for customers.
- **Expect to fail on the way**: early implementations may flop. Keep iterating until you find what works.
- **Examples at Amazon**
  - **Whole-cloth invention**: AWS and cloud computing, the Kindle digital book reader, and Alexa devices with speech recognition and natural language understanding.
  - **Marketplace (reinvention)**
    - **Externally aware**: saw customers responding to eBay and Half.com's broad third-party selection and range of prices.
    - **Internal resistance**: worried about relationships with distributors and publishers, and doubted third-party sellers would treat customers as well as Amazon did. Built it anyway, because wider selection and lower prices were better for customers.
    - **Failures first**: an eBay-style auctions site was a me-too product that failed. zShops, a separate section for third-party sellers, became a dead end nobody visited.
    - **The simplifying assumption**: put third-party offers on the same product detail pages as Amazon's own retail listings, where the traffic already was. Marketplace then took off.
    - **Result**: broader selection and lower prices for customers, and about 65% of units Amazon sells are now marketplace items.

## My example: UMD research lab image pipeline
- **Situation**: the lab produced 200–300 test images per day that had to be sorted by hand by honeycomb model, tension strength, and date.
- **Action**
  - Replaced manual sorting with an automated Python/PowerShell pipeline.
  - Simplified the categorization by reading the EXIF metadata embedded in each image instead of relying on filenames or manual inspection.
  - Split the model and tension values that were bundled together in the UserComment field.
  - Organized output into a simple model → tension → date folder hierarchy, and ran it on scheduled polling so it needed no manual trigger.
- **Result**: processed 1,200+ images per week and saved about 8 hours per week of manual work.
- **Invent and Simplify angle**: turned a repetitive manual process into a hands-off automated one by finding a simpler source of truth (embedded metadata).

# Are Right, A Lot

## Definition
- Leaders are right a lot. They have strong judgment and good instincts.
- They seek diverse perspectives and work to disconfirm their own beliefs.

## Key ideas
- **It's really about judgment**: you can do many things right, but getting the key decisions wrong for customers and the business causes real problems.
- **Amazon operates in ambiguity**
  - Often first to a market or inventing in a new space.
  - Even working businesses are constantly being changed and improved.
  - The job is to sift through the noise and find the signal: what really matters for customers.
- **Common misinterpretation**: being "right a lot" does NOT mean your idea has to win every debate.
- **The goal is the best answer, whoever's idea it is**
  - Get the right people in the room to give feedback.
  - Leaders often speak last so they hear everyone's input first.
  - Actively look for a different way of thinking than your going-in opinion.
- **Challenge your own beliefs**: question your most closely held views. Are they really right? Is there a better way for customers?
- **Ego doesn't matter**: in the best meetings, the team reaches the answer without the leader ever stating an opinion. The only thing that matters is the best outcome for customers.

## My example: [project]
- **Situation**: [a decision with incomplete information or a real disagreement]
- **Action**
  - [Your initial belief, and what made you question it]
  - [Who or what you sought out: data, teammates, a client, testing]
  - [How you weighed the options and decided]
- **Result**: [outcome, and whether the call proved right]
- **Are Right, A Lot angle**: made a sound call under ambiguity by seeking other perspectives and testing my own assumption instead of defending it.

# Learn and Be Curious

## Definition
- Leaders are never done learning and always seek to improve themselves.
- They are curious about new possibilities and act to explore them.

## Key ideas
- **The biggest career differentiator**: this principle most separates people who grow their careers from those who stagnate.
- **Stopping learning is decline**: the moment you think there's little left to learn is the moment you start unwinding as a professional. Be hungry to learn.
- **Simple, not easy**: with the right mindset it's straightforward. Accept that you don't know everything, and that areas you've studied for years can flip upside down quickly.
- **Change is part of the fun**: treat new learning as exciting, not threatening. Work would be boring if you already knew everything.
- **Self-assess honestly**
  - What am I doing well? What is the team doing well?
  - What do we need to get better at, based on what customers care about?
- **Talking isn't changing**: plenty of people talk well about what they'll learn and change but never actually do it. Build a real plan, then follow through.
- **Get a little better every day**: small, consistent improvement every day and every week.

## My example: Verbatim (video RAG platform)
- **Situation**: reviewing my resume, I found clear gaps: no Go, and no AWS services in my skills.
- **Action**
  - Built Verbatim, a RAG platform for YouTube videos and uploaded video files, for a Feather Software client, and chose Go specifically to learn the language on a project suited to its strengths (speed, low memory use, concurrent processing).
  - Used Go's standard library (net/http with Go 1.22+ routing) instead of a router framework, to learn the language's own tools first.
  - Deployed on AWS: Docker on EC2, PostgreSQL with pgvector on RDS, and S3 for media storage.
  - Learned RAG end to end: transcription (Whisper), chunking, embeddings, and vector similarity search.
- **Result**: [deployed for the client; add usage or performance numbers once you have them]
- **Learn and Be Curious angle**: honestly assessed my own gaps, made a concrete plan to close them, and followed through by shipping a real production project instead of just studying.

# Hire and Develop the Best

## Definition
- Leaders raise the performance bar with every hire and promotion.
- They recognize exceptional talent and willingly move people throughout the organization.
- Leaders develop leaders and take coaching others seriously.
- They build mechanisms for development, like Career Choice.

## Key ideas
- **Great results come from great teams**: nothing big and hard is built by one person.
- **"Great" means the leadership principles**: smart, right a lot, inventive, think big, dive deep, move fast, high ownership, customer obsessed.
- **Each interviewer in a hiring loop takes a leadership principle**: that's how Amazon defines and evaluates great people.
- **Never lower the bar**
  - Ask in every hiring decision: is this person at the bar? Do they raise it?
  - If no, don't hire, even under time pressure to staff a project.
  - Who we hire is one of the most important decisions made every day, week, and year.
- **Half hiring, half developing**: managers must be organized and thoughtful about what each person does well and where they need to grow.
- **Critical feedback matters**
  - Many companies now only praise strengths and "superpowers." Recognizing strengths is important, but it isn't enough.
  - People who want to learn and get better need to know their growth areas.
- **Managing is a privilege, not a right**: being a strong individual contributor doesn't mean you should manage. The privilege comes with the responsibility to actively coach your team.
- **The best managers aren't always the nicest**: the most impactful ones recognized strengths AND identified where you needed to grow to reach your full potential.

## My example: Eagle Scout service project
- **Situation**: led a 7-month community service project building picnic tables for a farm in Columbia, Maryland.
- **Action**
  - [How you recruited volunteers and matched people to tasks]
  - [How you taught or coached less experienced volunteers or younger scouts]
  - [Any feedback you gave, or how you raised the quality of the work]
- **Result**: [number of tables, volunteers, hours; what the people you led went on to do]
- **Hire and Develop the Best angle**: developed the people on my team by teaching skills and giving honest feedback so the work met a high bar.

# Insist on the Highest Standards

## Definition
- Leaders have relentlessly high standards, which many people may think are unreasonably high.
- They continually raise the bar and drive their teams to deliver high-quality products, services, and processes.
- They make sure defects don't get sent down the line and that problems are fixed so they stay fixed.

## Key ideas
- **Customers have very high expectations, and they should**: that's where Amazon sets the bar.
- **Switching is easy**: the internet makes it simple for customers to compare and leave, so you can't rest on past success.
- **"Unreasonably high" is the right level** for what Amazon is trying to accomplish.
- **Higher expectations lead to better results**: true at Amazon, with friends, with kids, and in any organization.
- **Model what good looks like**
  - As your scope grows, you can't be in every meeting.
  - Setting high standards in the meetings you're in is highly leveraged: people who see you model it carry it into the meetings you're not in, spreading it across the organization.
- **Standards slip and must be won back**: most companies, Amazon likely included, relaxed standards during the pandemic. Getting back to them is a fight worth fighting.
- **Companies that keep raising the bar win**: customers gravitate to companies that keep expanding what's possible for them.

## My example: Verbatim chunking bug
- **Situation**: Verbatim was returning low-quality answers and wrong timestamps, with no errors. It failed silently.
- **Action**
  - Didn't ship around it or accept "mostly works." Added logging to trace the chunking pipeline and spent about 5 hours finding the root cause.
  - Root cause: short transcript segments near chunk boundaries were getting cut off between chunks.
  - Fixed it at the source so it stayed fixed:
    - Carried a trailing-overlap tail across chunk boundaries.
    - Checked each segment's word count before adding it, and deferred it to the next chunk if it would push the current one over ~500 words, instead of splitting it.
- **Result**: [answer quality and timestamp accuracy after the fix; add a before/after measure if you have one]
- **Insist on the Highest Standards angle**: refused to accept a silent quality defect, found the real root cause, and fixed it so the problem couldn't come back.

# Think Big

## Definition
- Thinking small is a self-fulfilling prophecy.
- Leaders create and communicate a bold direction that inspires results.
- They think differently and look around corners for ways to serve customers.

## Key ideas
- **Look around corners**: never be content with where you are. Being a great inventor means seeing what's coming next.
- **Questions to keep asking**
  - What are the next big breakthroughs for customers?
  - What customer problem still needs solving?
  - How will the technology around the corner change the customer experience?
  - What will other companies build that customers will love, and how do we get there first?
- **Don't run the same playbook for decades**: a company built to last 100+ years has to keep changing course.
- **Change is hard even when it makes sense**: people resist taking risks or a new direction, which is why leaders who think big matter so much.
- **Bold initiatives aren't simple**, but they're how you serve customers better and make a unique impact.
- **Examples at Amazon**
  - **Delivery speed**: from many days → two days → one day → same day → a couple of hours or less with Prime Air drones.
  - **AWS**: inventing next-generation infrastructure with cloud computing.
  - **Broadband access**: connecting the 400–500 million households worldwide without broadband.
  - **Alexa**: building the world's most helpful personal assistant.
  - **Automotive**: reinventing how people buy and consume automotive products.
  - **Healthcare**: reinventing a customer experience that has long felt hopeless in the U.S.

## My example: [project]
- **Situation**: [the problem or opportunity, and what the "small" version would have been]
- **Action**
  - [The bigger vision you set, and why]
  - [How you communicated it or got others or clients on board]
  - [Risks you took to pursue it]
- **Result**: [what it led to]
- **Think Big angle**: [pushed past the obvious, incremental solution toward a bolder one that served customers better]

# Bias for Action

## Definition
- Speed matters in business.
- Many decisions and actions are reversible and don't need extensive study.
- We value calculated risk taking.

## Key ideas
- **Speed matters everywhere**: at every stage, in every industry, at every company size, unless you're a monopoly, and true monopolies barely exist anymore.
- **Speed is a choice, not a given**
  - Many enterprise CEOs claim they can't move fast because of security, compliance, size, or a slow culture. That isn't true.
  - Speed is a leadership and culture decision. If you prioritize it, you can move quickly even if you haven't before.
- **One-way vs. two-way doors**
  - **Two-way door**: if it's a mistake, you can walk right back out with no harm. This is the vast majority of decisions. Make them quickly and at the team level, thoughtfully but not recklessly, and reverse them if wrong.
  - **One-way door**: hard or impossible to reverse. These are rare. Take the time to think them through carefully.
- **Urgency**: don't take weeks to do what could be done in days or hours. It sounds obvious, but teams do it all the time.
- **Closing windows**: Amazon competes against the best-funded, most capable companies in land-rush races. Every week, ask: are my customers better off than when I started the week?
- **Tension with high standards**
  - Moving fast doesn't excuse a subpar customer experience. That would also violate Customer Obsession.
  - The leadership principles naturally conflict at times. Part of the job is finding the right balance.
  - You can be fast and keep high standards.
- **The world's biggest startup**: behave like a startup and keep asking why we can't move faster for customers.

## My example: Verbatim async ingestion
- **Situation**: Verbatim needed to process videos (transcribe, chunk, embed) without making users wait on the request.
- **Action**
  - Chose background goroutines over a full job queue to ship ingestion faster. It's a two-way door: the processing logic can move behind a queue later without a rewrite.
  - Kept it safe in the meantime with a 10-minute timeout and recover() for panic safety.
  - Knew and named the limitation: a server restart mid-processing leaves a video stuck in "processing," since nothing reconciles it on startup.
- **Result**: [shipped async ingestion to the client by X; the limitation hasn't caused issues / plan to add a queue]
- **Bias for Action angle**: treated a reversible infrastructure choice as a two-way door, shipped quickly with safeguards, and documented the known trade-off instead of over-engineering upfront.

# Frugality

## Definition
- Accomplish more with less.
- Constraints breed resourcefulness, self-sufficiency, and invention.
- There are no extra points for growing headcount, budget size, or fixed expense.

## Key ideas
- **Door desks**: Amazon has always used them as a signal to stay scrappy and skip anything extra.
- **Basis points matter**: Amazon was built on a single-digit-margin retail business, so every small saving counts (former CFO Mark Peek: he'd bend over for a penny).
- **Low margins are an advantage**
  - Constraints breed resourcefulness and invention.
  - They also make Amazon great at operating high-volume, low-margin businesses, which few tech companies can do.
- **Small teams, big results**
  - S3 and EC2 were each built by 13-person teams, while competitors had teams about 10x larger.
  - Those teams still built pioneering, market-leading products because the constraints forced them to be inventive.
  - Retail-trained operators helped AWS run cost-effectively at scale better than other tech companies.
- **Savings go back to customers**: money saved on everything funds lower prices and more capabilities.
- **Don't get numb to big numbers**
  - At $500B+ revenue, people start saying "it's only $100 million" or "I only need 65–70 people."
  - The best people, teams, and businesses do more with less.
  - Even in higher-margin businesses, don't spend more just because margins allow it.
- **Big teams aren't a career path**: Amazon values people who build great experiences and businesses as leanly as possible, including in promotions.

## My example: [project]
- **Situation**: [limited budget, time, or people]
- **Action**
  - [What you did instead of spending more or adding people]
  - [Specific cost-conscious choices and the reasoning behind them]
- **Result**: [what you delivered, and the cost or resources saved]
- **Frugality angle**: delivered a working result within tight constraints by being resourceful instead of adding cost.

# Earn Trust

## Definition
- Leaders listen attentively, speak candidly, and treat others respectfully.
- They are vocally self-critical, even when it's awkward or embarrassing.
- They don't believe their or their team's body odor smells of perfume.
- They benchmark themselves and their teams against the best.

## Key ideas
- **Common misinterpretation**: Earn Trust is NOT being nice, keeping social harmony, or agreeing not to challenge each other in meetings. Someone who challenges you in a group isn't untrustworthy.
- **What it actually means**
  - Be honest, authentic, and straightforward.
  - Listen intently, but challenge respectfully when you disagree.
  - Deliver what you said you would.
- **In practice**
  - If you say you've got something, deliver it.
  - If you think something is wrong for customers or the business, speak up.
  - If something you own isn't going well, say so, be self-critical, and fix it.
  - If you think the team isn't as good as it claims, benchmark it and prove it with data.
  - The reverse too: don't waste time beating yourself up if the data shows you're better than you think.
- **Jassy's OP1 story**
  - While presenting a 220-slide operating plan to the S-team, Jeff Bezos pointed out about 10 slides in that every number on one slide was wrong.
  - Jassy checked, realized Jeff was right, and admitted it on the spot. Jeff asked why he should trust the rest of the deck.
  - The rest of the deck had no more errors. Jassy wasn't resentful. He learned about diving deep and owning the details.
  - He earned trust back by owning the mistake, being openly self-critical, and delivering a more accurate presentation the next time to a broader group.

## My example: [project]
- **Situation**: [a mistake you made, or a time you had to deliver bad news or disagree]
- **Action**
  - [How you owned it openly instead of hiding or minimizing it]
  - [How you communicated it, and to whom]
  - [How you fixed it and made sure it didn't happen again]
- **Result**: [outcome, and how the relationship or trust held up]
- **Earn Trust angle**: owned my mistake candidly, fixed it, and delivered, which strengthened trust instead of damaging it.

# Dive Deep

## Definition
- Leaders operate at all levels, stay connected to the details, audit frequently, and are skeptical when metrics and anecdotes differ.
- No task is beneath them.

## Key ideas
- **Strategy AND details, not one or the other**: there can seem to be tension between Think Big and Dive Deep, but Amazon expects both.
- **Ideas are cheap, details are what matter**
  - Many people can fill whiteboards with great ideas but can't get the details right.
  - The details are what customers actually see.
  - Every Amazon product and business has been made or broken by how well the details were handled.
- **Narratives over PowerPoint**: slides let you stay high-level, but it's hard to fake details in a written narrative or working-backwards doc.
- **Inspect and audit**
  - Good leaders build mechanisms to inspect and audit details.
  - Strong teams understand that leaders diving in are helping them be right and get great results, not micromanaging.
- **Follow the anecdotes**
  - Big aggregate metrics (SLA performance, error rates, latency) can look fine across huge numbers.
  - A single complaint, a friend's story, or a customer email can reveal a real problem the metric hides.
  - At Amazon's scale, even a 0.5–1% impact means millions of people.

## My example: Verbatim chunking bug
- **Situation**: Verbatim wasn't throwing errors, and nothing looked broken at a high level. But answers were low quality and timestamps were wrong.
- **Action**
  - Treated the bad answers as a signal of a real problem instead of blaming the model.
  - Added logging through the chunking pipeline to inspect what was actually being stored in each chunk.
  - Traced the cause to the details: short transcript segments near chunk boundaries were being cut off between chunks.
  - Fixed it at the root:
    - Carried a trailing-overlap tail across chunk boundaries.
    - Checked each segment's word count before adding it, and deferred it to the next chunk if it would push the current one over ~500 words, instead of splitting it.
- **Result**: [answer quality and timestamp accuracy after the fix; add a before/after measure if you have one]
- **Dive Deep angle**: didn't trust surface-level "it's working." Followed the bad outputs down to the exact chunk boundaries, found a silent defect, and fixed the root cause.

# Have Backbone; Disagree and Commit

## Definition
- Leaders are obligated to respectfully challenge decisions when they disagree, even when it's uncomfortable or exhausting.
- They have conviction and are tenacious.
- They don't compromise for the sake of social cohesion.
- Once a decision is made, they commit wholly.

## Key ideas
- **Speaking up is expected, not just allowed**: at every level, if you think something is wrong for customers or the business, say so.
- **"I told you so" is useless**: it always means a failure. Either you didn't speak up when you should have (no backbone), or you didn't fully commit after the decision (no commitment).
- **Don't compromise for social cohesion**
  - People often compromise just to get along.
  - Ceiling example: one person says 10 ft, the other says 14 ft, so they settle on 12 ft. But it's usually not 12 ft. There's an answer closer to the truth.
  - Real issues are more nuanced, but the point stands: be truth-seeking, not peace-keeping.
- **Debate fully, then commit wholly**
  - Hard issues may be debated across many meetings and weeks.
  - Once decided, everyone commits fully, including people who argued the other side.
- **Why commitment is hard but necessary**
  - Amazon hires smart, passionate people, and it's hard to let go of what you believe is best for customers.
  - Businesses that can't make decisions stagnate.
  - With huge opportunity spaces and capable competitors, everyone's energy has to go in the same direction.

## My example: [project]
- **Situation**: [a decision you disagreed with: client, teammate, manager, professor]
- **Action**
  - [How you raised the disagreement respectfully, with data or reasoning]
  - [How the decision was made, and whether it went your way]
  - [How you committed fully once it was decided]
- **Result**: [outcome of the decision and of your commitment]
- **Disagree and Commit angle**: challenged the decision respectfully with reasoning, then fully committed and delivered once it was made.

# Deliver Results

## Definition
- Leaders focus on the key inputs for their business and deliver them with the right quality and on time.
- Despite setbacks, they rise to the occasion and never settle.

## Key ideas
- **Nothing else matters if you don't deliver**: you can be customer obsessed, inventive, strategic, detail-oriented, and fast, but if you fail to deliver, none of it counts. Delivery is where it reaches customers.
- **Outputs vs. inputs**
  - **Outputs**: high-level metrics like stock price, free cash flow, revenue, and operating margin. They're important, but you can't actively manage them.
  - **Inputs**: the actual initiatives that change the customer experience. These drive the outputs, and they're what you can actually control.
  - Amazon's key goals, up to the S-team, are almost entirely inputs.
- **Staring at outputs doesn't change them**: Jassy's old manager watched daily sales tick up and down on his monitor. It mattered, but looking at it couldn't move it.
- **Launch is the starting line, not the finish line**
  - Getting to launch takes huge effort (defining the product, working-backwards docs, hiring, constant changes), so people exhale and feel done.
  - Almost nothing at Amazon was a breakaway hit at first launch.
  - Launch, see how customers react, get feedback, and iterate.
  - The best teams launch fast and organized, then keep iterating. After 7–9 iterations, you have something that really matters to customers.

## My example: UMD research lab image pipeline
- **Situation**: the lab generated 200–300 test images per day that had to be sorted by hand by honeycomb model, tension strength, and date.
- **Action**
  - Built and shipped an automated Python/PowerShell pipeline that read EXIF metadata and sorted images into model → tension → date folders.
  - Ran it on scheduled polling so it kept processing new images continuously.
  - Handled failures: unreadable images were caught, logged, and moved to a separate folder instead of breaking the run.
  - [A setback you hit while building it, and how you got past it]
  - [Any iteration after the first version went live]
- **Result**: processed 1,200+ images per week and saved about 8 hours per week of manual work.
- **Deliver Results angle**: delivered a working, reliable tool with measurable impact, and kept it running as new data came in.

# Strive to be Earth's Best Employer

## Definition
- Leaders work every day to create a safer, more productive, higher-performing, more diverse, and more just work environment.
- They lead with empathy, have fun at work, and make it easy for others to have fun.
- They ask: Are my fellow employees growing? Are they empowered? Are they ready for what's next?
- They have a vision for and commitment to employees' personal success, whether at Amazon or elsewhere.

## Key ideas
- **One of the two newest principles**: broad, and often interpreted many different ways.
- **It doesn't mean doing everything employees ask**: the company can't be all things to everyone, so not pursuing a request doesn't mean Amazon has failed this principle.
- **What makes a great place to work, in Jassy's view**
  - **An inspiring mission**: making customers' lives easier and better every day, and actually doing it.
  - **Scale**: making that impact for a very large number of customers.
  - **Invention**: inventing and betting on customers instead of running the same playbook for years.
  - **Long-term commitment**: sticking with investments instead of running at the first lack of traction.
  - **Great teammates**: smart, passionate, motivated people working together on a shared mission.
- **Room to improve**: safety in the fulfillment network, better manager training for developing people's careers, and a more diverse and inclusive workforce.

## My example: [project]
- **Situation**: [a team or group you were part of or led]
- **Action**
  - [How you made the environment better for others: inclusion, support, growth, morale]
  - [How you helped someone grow or feel empowered]
- **Result**: [impact on the people and on the work]
- **Earth's Best Employer angle**: improved the environment for the people around me so they could grow and do their best work.

# Success and Scale Bring Broad Responsibility

## Definition
- Amazon started in a garage but isn't there anymore. It's big, it impacts the world, and it's far from perfect.
- Leaders must be humble and thoughtful about even the secondary effects of their actions.
- Local communities, the planet, and future generations need Amazon to be better every day.
- Begin each day determined to make better, do better, and be better for customers, employees, partners, and the world, and end each day knowing you can do more tomorrow.
- Leaders create more than they consume and always leave things better than they found them.

## Key ideas
- **Be a great community member**, in both narrow and broad communities.
- **Keep asking**: are the communities we're in better off because we're there? If not, take action.
- **More than jobs**: contribute to the fabric of communities, not just employment.
- **Examples at Amazon**
  - **Affordable housing**: $1.8B+ invested in the Puget Sound, Arlington (VA), and Nashville areas.
  - **Homelessness**: partnership with Mary's Place in Puget Sound, housing 200+ family members in Amazon's corporate buildings every night (1,000+ per year).
  - **Food security**: partnered with 35 cities to serve 10M+ free meals to 80,000+ families.
  - **Education**: philanthropic efforts reached 3.9M+ people in 9 countries in a year; Amazon Future Engineer committed $16M in 400+ scholarships for students pursuing tech careers.
  - **Disaster relief**: 23M+ relief items delivered across 44 incidents in a year.
  - **Volunteering**: 150,000+ Amazonians volunteered in a year.
- **Evolution**: Amazon waited until it was profitable to invest heavily in communities, and has since become the top corporate giver in Puget Sound.

## My example: Eagle Scout service project
- **Situation**: [what the farm in Columbia, Maryland needed, and why it mattered to the community]
- **Action**
  - Led a 7-month community service project building picnic tables for the farm.
  - [How you planned it, gathered materials or funding, and organized volunteers]
- **Result**: [number of tables built, number of volunteers, how the farm and community use them]
- **Broad Responsibility angle**: used my skills and leadership to leave a community resource better than I found it.