# LangGraph Memory Conversational Agent 
## Overview

This project demonstrates a minimal conversational AI agent built with LangGraph and LangChain using OpenAI's GPT model.
The agent processes user messages through a simple workflow graph, maintains conversation history, and stores the full interaction in a log file.

The goal of the project is to illustrate how state-based agent workflows can be implemented using LangGraph while preserving a clean and extensible architecture.

## Features

Interactive command-line AI conversation

Built with LangGraph state-based workflows

Maintains conversation history across turns

Uses OpenAI GPT models through LangChain

Automatically saves the entire conversation to a log file

## How It Works

The system uses a state graph where the conversation state is passed between nodes.

### State Definition

The agent state contains a list of conversation messages.
``` python
class AgentState(TypedDict):
    messages: List[Union[HumanMessage, AIMessage]]
```   
## Processing Node

The processing node sends the conversation history to the language model and appends the response to the state.
```python
def generate_response(state: AgentState) -> AgentState:
    response = llm.invoke(state["messages"])
    state["messages"].append(AIMessage(content=response.content))
    print(f"\nAI: {response.content}")
    return state
```
## Graph Workflow

## A simple graph pipeline is defined:

`START → process → END`

This makes it easy to extend later with:

tool nodes

memory nodes

retrieval systems

multi-agent flows

## Project Structure
langgraph-agent/
│
├── app.py
├── conve_history.txt
├── requirements.txt
├── .env
├── .gitignore
└── README.md

`app.py`
Main program containing the agent graph and CLI interaction.

conve_history.txt
Automatically generated conversation log.

## Installation

Clone the repository:

git clone https://github.com/yourusername/langgraph-agent.git
cd langgraph-agent

Install dependencies:
`pip install -r requirements.txt`

Environment Setup

Create a .env file and add your OpenAI API key:

OPENAI_API_KEY=your_api_key_here

The project uses python-dotenv to automatically load environment variables.

## Running the Agent

Start the agent:

`python app.py`

Example interaction:

Enter: What is machine learning?

AI: Machine learning is a field of artificial intelligence that enables systems to learn patterns from data and improve over time without explicit programming.

Type exit to stop the program.

### After exiting, the conversation will be saved to:

conve_history.txt