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
- **Are right, A Lot**
- **Learn and Be Curious**
- **Hire and Develop the Best**
- **Insist on the Highest Standards**
- **Think Big**
- **Bias for Action**
- **Frugality**
- **Earn Trust**
- **Dive Deep**
- **Have Backbone; Disagree and Commit**
- **Deliver Results**
- **Strive to be Earth's Best Employer**
- **Success and Scale Bring Broad Responsbility**
- 