# Parser
Company realised that we need to finally move to a proper frontend framework and to expedite it, a consultancy was hired to transform one part of our platform into this new better workflow. I was set up as a backend resource in that team to have in depth understanding of the delivery. My role shifted very quickly form that to actually tech leading the team and ensuring alignment between this new delivery and whats best for the company.

# Data input validation overhaul
After our company implemented initiative to increase co-working across the teams, I suggested to volunteer in CS team, which are our main internal client
I've noticed the big pain point - usually the data that comes in goes through several loops of being uploaded, failing validation and then being reuploaded again. If validation succeeds, it goes on to run the model, where it still might fail. This pain point was known to PM team but it wasn't top priority in the list and also they weren't sure what could be done about it, it was taken like a normal thing. 
However, it was clear to me that a solution which provides a more in depth validation and faster was neccessary. I did my research and proposed a move to pandera - pandas validation library. This has cut the validation time up to 100x and enabled users to validate data in seconds and perform much more in depth validation checks. I presented it to key stakeholders and they were excited with a much needed overhaul to the validation and potential posibilities of early failure it would bring. I think my main takeways from this experience is that importance of direct (software to client) look and always being eager to improve the current situation. 

# Transition planner updates
We had a part of the platform where it wasn't used heavily but one of our biggest clients were using it actively. (explain transition planning platform). When it was coming to the release, PM informed us that the client want some changes but they are not sure how this will be delivered as they will have a workshop quite close to release (few days before testing period, 1-2 weeks before release). Delaying the release due to this wasn't an option as we had to update some security packages and untangling everything would've been very hard.
I proposed that to utilise resource until requirements are known the prep must be done:
- I've refactored the part of the platform, to make it much easier to update
- Together with PM we went through likely scenarios and I implemented skeleton for them
- I prepped the model code for our climate scientist to upgrade once the requirements are in
- We free up necessary resource for when the requirements come in
This lead to the final implementation taking just a couple days and successful release of the platform. In the end client was happy and we did some much needed refactor.
My main takeway from this story is that if the requirements are unknown, in most cases you can guess big chunk of the workflow and prep for that. Also it's a good time to make sure the part where the changes are coming in is very extendable. Also some teammates were holding firm stance on we need more time / we agreed not to have this come in late but I understand that product only did this as it was necessary and also it was our biggest client, making them happy was important for the business.


# Failure - roll out pandera everywhere
If not told the top story, retell some context.
Next logical step is to roll it out to the models themselves. Moreover, it would be great to have pandera schemas both for inputs and outputs of the models. This would help us few fold:
- More trust in what model produces
- Easier to develop frontend/backend when we know the schemas
- Have a nice library of schemas that move across models and inform of our data structures.
I've proposed doing this for the next round of model updates and said I will collaborate with modellers to do it for one of the models so it would be an example.
We did implement it to the model but it required a significant effort to update when model was still in development. Moreover, I was the person with a stick, so I had to keep in check that modellers are doing that and it was a lot of effort and hard to push back especially when models are key release item and these checks are nice to have. moreover the team was still new to pandera so I was the person with the knowledge
This resulted in only some models going out with schemas.
When I look back at this, I realise that few things would've made a massive difference:
- Prepping team for pandera and splitting the load
- Adding CI checks for pandera schemas - it is easier to say fails CI than manual explanations of why this is not good
- Making sure there's additional time allocated in the usual process for this new step
