---
layout: post
title:      "FootBit. A Rails Application."
date:       2020-06-16 01:55:03 +0000
permalink:  footbit_a_rails_application
---

FootBit is a rails application that connects Soccer Agents and players looking for try out opportunities with professional teams. In the professional sports world it is very hard to build connections and create opportunities. FootBit provides a simple, easy to use playform for agents and players to connect. It will provide an equal playing field for all potential prospects. No longer will it be "who you know" to get an opportunity. It will be who is the best and most qualified. 

This is an important step for the world of soccer. Players from all over the world, no matter rich or poor will all have the same opportunities to achieve their dreams. In addition, It is a great way for agents to recruit players to their agency and grow their talent pool. 

**How it all works:**

In a way, FootBit can be compared to websites like Craigslist. An agent can create a profile and create a new "team" instance. For which he then may create a tryout for. This brings us to the **models.**

A **User**, in this case the agent can have **many tryouts** and **many teams *through**  **tryouts.**
A **Team** can have **many tryouts** and ***many users** through* **tryouts.**
A **Tryout** belongs to a **team and User.**

Therefore, agents can create multiple tryouts for the same team. This is great for increasing competition. We all know competition is an essential part of success and growth. 
