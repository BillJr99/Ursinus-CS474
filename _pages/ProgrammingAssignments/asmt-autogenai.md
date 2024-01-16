---
layout: assignment
permalink: /Assignments/Programming/AutoGenAI
title: "CS474: Human Computer Interaction - AI Agents using AutoGen and OpenAI"
excerpt: "CS474: Human Computer Interaction - AI Agents using AutoGen and OpenAI"

info:
  coursenum: CS474
  points: 100
  goals:
    - "Experiment with building, defining, and customizing agents and skills in AutoGen Studio."
    - "Create and run a session in AutoGen Studio's Playground using a predefined workflow."
    - "Comprehend the principles and methods of creating custom agents programmatically using the AutoGen library."
    - "Implement a custom AI solution using AutoGen, focusing on a specific application."
    - "Evaluate the capabilities and limitations of retrieval-augmented generation agents within the AutoGen framework."
    
  rubric:
    - weight: 15
      description: Implementation and Functionality of Code Solution
      preemerging: The code solution is non-functional or demonstrates significant errors.
      beginning: The code solution is functional but lacks complexity and shows minimal customization.
      progressing: The code solution is well-implemented with good functionality and some level of customization.
      proficient: The code solution is excellently implemented, showing high functionality, customization, and innovation.
    - weight: 15
      description: Reflective Write-Up on Personalization and Usability
      preemerging: Reflective write-up lacks insight into personalization and usability aspects of the solution.
      beginning: Basic reflection on personalization and usability, but lacks depth and critical analysis.
      progressing: Good reflection, providing insights into personalization and usability with relevant examples.
      proficient: In-depth and insightful reflection on personalization and usability, demonstrating comprehensive understanding.
    - weight: 10
      description: Reflection on Ethical Considerations of Automated Systems
      preemerging: Minimal or no reflection on the ethical implications of using automated systems.
      beginning: Basic understanding of ethical considerations, but lacks depth and practical insights.
      progressing: Good reflection on ethical considerations, showing understanding of implications and responsibilities.
      proficient: In-depth reflection on ethical considerations, demonstrating a comprehensive and responsible approach to automated systems.
    - weight: 20
      description: Understanding and Application of AutoGen Framework
      preemerging: Limited or no understanding of the AutoGen framework's capabilities and functionalities.
      beginning: Basic understanding of AutoGen's role in AI agent creation but struggles with practical application.
      progressing: Good grasp of AutoGen functionalities and can apply them in creating simple AI agents.
      proficient: Demonstrates in-depth understanding and adept application of AutoGen in creating complex AI agents.
    - weight: 15
      description: Installation and Utilization of AutoGen Studio
      preemerging: Unable to install or navigate through AutoGen Studio.
      beginning: Successfully installs AutoGen Studio but faces challenges in navigation and utilization.
      progressing: Comfortably installs and navigates AutoGen Studio, using basic features effectively.
      proficient: Exhibits expertise in installing, navigating, and fully utilizing all features of AutoGen Studio.
    - weight: 20
      description: Creation and Customization of Agents and Skills
      preemerging: Shows minimal understanding and ability in creating or customizing agents and skills.
      beginning: Can create basic agents and skills but lacks customization depth.
      progressing: Good competency in creating and customizing agents and skills with some complexity.
      proficient: Excels in creating highly customized and complex agents and skills, demonstrating innovative thinking.

  readings:
    - rtitle: "AutoGen Studio - Interactively Explore Multi-Agent Workflows"
      rlink: "https://microsoft.github.io/autogen/blog/2023/12/01/AutoGenStudio/"
    - rtitle: "AutoGen Studio"
      rlink: "https://github.com/microsoft/autogen/tree/main/samples/apps/autogen-studio"
    - rlink: "https://microsoft.github.io/autogen/docs/Use-Cases/agent_chat/#diverse-applications-implemented-with-autogen"
      rtitle: "Multi-agent Conversation Framework"
    - rlink: "https://www.mlq.ai/building-ai-agents-autogen/"
      rtitle: "Building AI Agents with AutoGen"
    - rlink: "https://microsoft.github.io/autogen/blog/2023/10/18/RetrieveChat/"
      rtitle: "Retrieval-Augmented Generation (RAG) Applications with AutoGen"
      
tags:
  - ai
  - gpt
  
---

In recent years, AI has transformed from an estimator/predictor to a creator with the advent of generative AI.  With the progression of agent systems, AI has become a "doer" capable of engaging multiple personas (or "agents") in conversatios oriented around problem solving.  In this assignment, we will explore the creation of custom AI agents, and develop our own personalized AI solution. 

## Part 1 - Introduction to AutoGen

[AutoGen](https://github.com/microsoft/autogen) is a Microsoft framework that allows you to define various agents that can interact with one another to solve problems using AI.  They can prompt the user for context and input that they use to work together to solve a problem according to a workflow that you can customize.  For example, whereas traditional Chat GPT can create text to respond to questions, an agent can take a problem statement and call functions, invoke APIs, and converse with other agents to provide custom solutions to your inquiry.  

### AutoGen Studio - A No-Code Solution

You can specify AutoGen agent behaviors, and invoke those behaviors, in Python.  However, there is also a no-code solution called [AutoGen Studio](https://github.com/microsoft/autogen/tree/main/samples/apps/autogen-studio) in which you can add skills, define agents, and chat with the resulting system using a web interface.  You can install this web interface directly within your local environment.  To do this, run:

```
pip install autogenstudio
export OPENAI_API_KEY=<your key here>
autogenstudio ui --port 8081
```

An API key will be provided to you for use in this class.  Please shut down your applications when you're not using them, to avoid incurring additional charges against this API key!  Your instructor is funding this API key directly, and is sharing it with the entire class.  Please be judicious about its usage.  You are welcome to create an account and key for yourself for further exploration, but this is not required for this class.

To try it out, click on the **Build** tab and select **Skills** from the left menu.  You can click on the sample skills to view the code that drives each.  Notice that each invokes a custom API to answer your question (such as scraping a web page, or writing code to create visualizations in `matplotlib`, etc.).  Agents can invoke these skills, which you can think of as functions, to answer questions.

In the **Agents** menu, you can create your own custom agents.  It's possible to do this directly from the **Workflows** section, so just take a look at some of the provided agents for now.  Notice that they can import skills as well as language models like `gpt-4` to answer questions.

In the **Workflows** menu, you can connect an agent to skills by selecting each through the menu.  Try creating one of your own that uses some of the example skills provided.  In this example, we'll use the **Visualization Workflow** which uses the **Visualization Agent** to generate plots using `matplotlib` in Python.

#### Creating a Session

Click on the **Playground** Tab, and click **New** under **Sessions** on the left menu.  Choose the **Visualization Workflow**, and ask it the following query (from the [Microsoft autogen GitHub repository tutorial page](https://github.com/microsoft/autogen/tree/main/samples/apps/autogen-studio)):

```
Plot a chart of NVDA and TESLA stock price YTD from January 1 of this year to the current date. Save the result to a file named nvda_tesla.png
```

Simply paste this query into the workflow chat page, and give it a few moments to execute.  The chatbot will install Python dependencies for `matplotlib` and other libraries, so this will take a few minutes, but you'll see a plot of the stock when it is finished!

Click below the image to expand the messages.  It provides not only the image that it saved to your session, but also the code that it generated to execute your request.  The agent ran that code automatically.  Sometimes, agents will require more information from the user, and it will ask you questions that you can type in just as with a traditional GPT.  In this case, no such additional information should be needed to answer your query, so you should just see the result.

#### Creating Custom Skills

Go back to the **Skills** menu under the **Build** tab.  You can click **New** to create a new Skill, which provides the agent additional functionality that it can execute.

Here is a simple example that generates a random story given a theme.  It's not terribly creative as this is a deliberately minimal example, but you could imagine substituting API calls here to execute outside functionality.  Try pasting this into a new Skill definition, and give your Skill a name.

```python
import random

def generate_story(theme):
    """
    Generates a short story based on the given theme.

    Args:
    theme (str): The theme of the story.

    Returns:
    str: A short story.
    """

    # Sample beginnings, middles, and endings for the story
    beginnings = [
        "Once upon a time, in a distant land, ",
        "In a small village, surrounded by mountains, ",
        "In a futuristic city, where technology ruled, "
    ]

    middles = [
        "a young hero decided to embark on a journey, ",
        "an unexpected event turned everything upside down, ",
        "a mysterious figure appeared, offering a challenge, "
    ]

    endings = [
        "and thus, the adventure came to a joyful end.",
        "which led to unexpected friendships and lessons learned.",
        "and the hero's courage changed their world forever."
    ]

    # Randomly select parts of the story
    beginning = random.choice(beginnings)
    middle = random.choice(middles)
    ending = random.choice(endings)

    # Combine the parts to form the story
    story = f"{beginning}when {theme}, {middle}{ending}"

    return story
```

Now, create a new workflow, and when it asks you to specify the Agent, click on the button to customize the Agent.  Under the list of skills you will see an **Add** button, and you can add this new Skill to the list that it can execute.

Go back to the **Playground** and set up a Session with this new workflow.  Tell it to tell you a story about something (you can make up what it is).  The chatbot will take your theme, pass it as a parameter to the skill, and provide you with the response!

### Creating Custom Agents with AutoGen

AutoGen Studio is a front-end user interface to AutoGen, but you can create these agents programmatically directly through the AutoGen library.  To do this, we will first provide our OpenAI API key similar to the way we did before.  This time, we'll add the key to a dictionary file, which we'll load in our Python program.  Create a file called `OAI_CONFIG_LIST` and populate it as follows:

```
[
    {
        "model": "gpt-4",
        "api_key": "<your api key here>"
    }
]
```

In addition, create a working directory for the chatbot to store files.  We'll call ours `work`:

```
mkdir work
```

Now, your Python program can do the following:

```python
from autogen import AssistantAgent, UserProxyAgent, config_list_from_json

config_list = autogen.config_list_from_json(
    env_or_file="OAI_CONFIG_LIST",
    file_location=".",
    filter_dict={
        "model": {
            "gpt-4",
            "gpt4",
            "gpt-4-32k",
            "gpt-4-32k-0314",
            "gpt-35-turbo",
            "gpt-3.5-turbo",
        }
    },
)
assistant = AssistantAgent("assistant", llm_config={"config_list": config_list})
user_proxy = UserProxyAgent("user_proxy", code_execution_config={"work_dir": "work"})
user_proxy.initiate_chat(assistant, message="Plot a chart of NVDA and TESLA stock price YTD from January 1 of this year to the current date.")
```

This creates the agent (`assistant`), configured with our API key by passing it the filename in which the key is provided, and the user proxy agent (`user_proxy`) which acts as the user typing in questions to the chatbot agent.  Calling `initiate_chat` will pass the message to the chatbot agent, and any followup questions will be prompted to you by the `user_proxy` agent.  Otherwise, the result will appear on-screen.  Of course, this is a console application, so the plot won't appear like it did with AutoGen Studio.  Instead, it will provide you the code that you can execute to generate the plot for yourself, and if the agent is able to execute that code, it will output the plot file to your working directory (called `work`).

### Creating Custom Skills

These agents can also provide custom functionality similar to the "Skills" we saw in the AutoGen Studio UI.  Here, they're just functions.

Start out by defining your `config_list` as before to specify your OpenAI API key, and import the following packages:

```python
import json
import os
from typing_extensions import Annotated

import autogen
from autogen import AssistantAgent, UserProxyAgent
```

This time, we'll specify an LLM configuration dictionary that specifies a timeout for calling these custom functions, and we'll pass our `config_list` to that to initialize this particular agent (from the [Microsoft autogen documentation](https://microsoft.github.io/autogen/docs/Use-Cases/agent_chat/#diverse-applications-implemented-with-autogen)):

```python
llm_config = {
    "config_list": config_list,
    "cache_seed": 42,
    "timeout": 120,
}
```

Now, you can create an assistant agent and a user proxy agent, just like before, but we'll specify some custom behaviors (from the [Microsoft autogen documentation](https://microsoft.github.io/autogen/docs/Use-Cases/agent_chat/#diverse-applications-implemented-with-autogen)):

```python
chatbot = autogen.AssistantAgent(
        name="chatbot",
        system_message="You are a chatbot assistant that generates a random number using only the function provided.  Reply with TERMINATE when your task is done.",
        llm_config=llm_config
)

user_proxy = autogen.UserProxyAgent(
        name="user_proxy",
        is_termination_msg=lambda x: x.get("content", "") and x.get("content", "").rstrip().endswith("TERMINATE"),
        human_input_mode="NEVER", # or ALWAYS by default
        max_consecutive_auto_reply=10
)
```

The `system_message` allows you to tell the chatbot more about itself.  You could make it a professor, a student, a travel agent, or anything you can imagine.  Here, we'll tell the agent that it should execute a custom function that we will provide it in order to answer questions.  To help us determine when the response has ended, we'll tell it to respond with the word "TERMINATE" when it has finished.

The `user_proxy` specifies an `is_termination_msg` function that returns true when the message ends with the word `TERMINATE`.  Since we told the agent to respond with `TERMINATE` when it is finished, this gives us an easy way to know when to stop providing input to the chatbot agent.  We also tell it that it can converse with the user agent up to 10 times before finishing.  In this simple example, we will likely never reach that limit.

Additionally, there is a parameter `human_input_mode` which is set to `NEVER`.  This can be changed to `ALWAYS` (or removed as `ALWAYS` is the default) to allow the chatbot to prompt the user with questions for feedback or additional context.

Next, let's provide a custom function to the chatbot, to give it a "Skill" like we did earlier:

```python
@user_proxy.register_for_execution()
@chatbot.register_for_llm(description="Random number generator.")
def gen_random(n: Annotated[int, "Upper limit for random number generation"]) -> str:
    import random
    value = random.randint(0, n)
    return f"{value}"
```

This minimal example tells the agent that it can call the `gen_random` function to compute a random number up to a certain threshold, given as a parameter.  The agent will extract this parameter from your input message, and pass it to the function automatically.

Finally, initiate the chatbot as follows:

```python
user_proxy.initiate_chat(
        chatbot,
        message="Generate 5 random numbers up to 100"
)
```

### Retrieval-Augmented Generation Agents with AutoGen

You can also provide your own knowledge base documents that the agent can use to formulate its responses.  For example, we could download the [Ursinus course catalog](https://www.ursinus.edu/live/files/5040-catalog-2023) as a PDF, and save it in a `docs` subdirectory of our project, and our agent would read that document and use it to formulate responses.  We could populate this directory with other documents as well (for example, past course catalogs).

As before, set up your `config_list` and `llm_config` variables, and import the following packages:

```python
import json
import os

import autogen
from autogen.agentchat.contrib.retrieve_assistant_agent import RetrieveAssistantAgent
from autogen.agentchat.contrib.retrieve_user_proxy_agent import RetrieveUserProxyAgent
```

And, as before, create your chatbot and user proxy agents (from the [Microsoft autogen blog post about Retrieval-Augmented Generation (RAG)](https://microsoft.github.io/autogen/docs/Use-Cases/agent_chat/#diverse-applications-implemented-with-autogen)):

```python
assistant = RetrieveAssistantAgent(
    name="assistant",
    system_message="You are a helpful assistant.",
    llm_config=llm_config,
    },
)

ragproxyagent = RetrieveUserProxyAgent(
    name="ragproxyagent",
    max_consecutive_auto_reply=3,
    retrieve_config={
        "task": "qa",
        "docs_path": [
            os.path.join(os.path.abspath(""), "docs"),
        ]
    }
)
```

This agent reads documents from the docs directory, under the current directory.  Now, you can interact with the agent like before:

```python
assistant.reset()
userproxyagent = autogen.UserProxyAgent(name="userproxyagent")
ragproxyagent.initiate_chat(assistant, problem="Recommend courses based on my interest in Machine Learning and Biomedicine")
```

Since the catalog knows when courses are generally offered, and what prerequisites courses have, etc., you could ask it more interesting questions like "Suggest courses for the Fall Semester of 2024 for a Computer Science major."  Additionally, you could add documents to the knowledge base repository that provide information about major requirements.  `docs_path` supports URL's, so you could provide it the URL of the course major page itself and create a "virtual advisor" agent.

## Part 2 - Developing Your own AI Solution

Using the AutoGen AI Studio or the AutoGen library, create a custom agent with skills for a personalized solution (for example, a "virtual academic advisor," or a programming tutor, etc.).  Write up a tutorial to re-create your solution, and ask another student to execute queries against your chatbot.  Record which queries they execute and your responses, and discuss ways in which you could add additional personalization capabilities to your solution.  In addition reflect upon the ethical considerations of using your solution.  For example, what could go wrong by replacing a faculty advisor with a virtual one; does this mean one should not use a virtual advising solution at all?