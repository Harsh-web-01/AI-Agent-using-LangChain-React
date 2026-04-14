# LangChain ReAct Agent: Web Search & Weather Assistant

This project consists of a simple, yet powerful end-to-end AI Agent built using the LangChain. This project demonstrates how to implement a **ReAct (Reasoning and Acting)** agent capable of querying the web and fetching live weather data to answer complex user prompts.

## 🚀 Features

- **ReAct Agent Architecture**: Uses the ReAct prompting strategy (`hwchase17/react` from LangChain Hub) to instruct the LLM on how to reason through a problem and take sequential actions.
- **Web Search Integration**: Uses the `DuckDuckGoSearchRun` tool to allow the agent to look up real-time information on the internet.
- **Custom APIs**: Includes a custom `get_weather_data` tool that connects to the [Weatherstack API](https://weatherstack.com/) to fetch real-time weather information for any city gracefully.
- **LLM Powered**: Built around the OpenAI language models using `ChatOpenAI`.

## 🛠 Prerequisites

Before running the agent, make sure you have the following API keys:
1. **OpenAI API Key**: Required for the `ChatOpenAI` LLM.
2. **Weatherstack API Key**: Required for the custom weather tool.

### Example Prompt

The default prompt in the script is:
> *"Find the capital of Madhya Pradesh, then find it's current weather condition"*

### How it works:
1. **Thought**: The agent reads the input and decides it first needs to know the capital of Madhya Pradesh.
2. **Action**: It uses the `duckduckgo_search` tool to look it up.
3. **Observation**: It learns the capital is Bhopal.
4. **Thought**: It now needs to find the weather for Bhopal.
5. **Action**: It uses the custom `get_weather_data` tool, passing "Bhopal" as the argument.
6. **Observation**: It receives the JSON response from Weatherstack.
7. **Final Answer**: It formats the gathered information into a readable sentence for the user.

## 📂 Code Walkthrough (`agent.py`)

- **Tools Definition**: The agent uses `search_tool` (DuckDuckGo) and an `@tool` decorated function `get_weather_data` that utilizes the python `requests` library to fetch JSON data.
- **Agent Initialization**: The standard ReAct prompt is pulled from `hub.pull("hwchase17/react")` and wrapped along with the tools and LLM using `create_react_agent()`.
- **Execution**: The `AgentExecutor` manages the execution loop, parsing the agent's output and executing the right tools until the final answer is reached.

## 📌 Conclusion
This project showcases how to build an intelligent AI agent capable of thinking, acting, and learning from observations.
Unlike traditional LLM applications, this agent follows a structured reasoning loop, making it significantly more powerful for solving complex, real-world problems.
