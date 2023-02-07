*Written on: 10 August 2022*

# Initial Design

The purpose of this document is to articulate the requirements and design of the service Atlas, software developed for the AIDED research project.

# Background

At the current state of the software team of AIDED, there is not much documentation as to what is required and what the goals are of the team.  This document aims to fill that gap and provide access to the software team’s goals, the details of how the goals will be met, and to provide an overview of what is in-scope vs. out-of-scope of the project. 

# Requirements

The requirements of the service are as follows

1.  Send the following information to Hermes
	1. Destination data
2. Receive the following information from Hermes
	1. Drone location
3.  Store information about
	1. Hermes’ current flight and location
	2. Public transportation in the city of East Lansing
	3. Completed and uncompleted trips
4. Compute efficient routes based on the currently pending jobs
  

# Implementation

The service will be designed and implemented in a way to promote easy extensibility in the future.  Using design patterns, well-formatted and commented code, and avoiding hardcoding important information are all things that will be focused on when implementing Atlas.

Atlas will be split into 3 major parts

1.  An API hosted by Heroku
2.  A PostgreSQL database hosted by Heroku
3.  A client-side script

##### API

The API will be hosted by Heroku and will be built with Python and Flask.  This will connect the client-side script and the PostgreSQL database.  The script will be able to update the database with new information and will also receive information about which jobs to send to Hermes by using the endpoints of the API.

##### Database

The database will be a PostgreSQL database hosted by Heroku.  This allows for the API and database to talk to each other easily since both are hosted on Heroku.  Read more about Heroku PostgreSQL [here](https://www.heroku.com/postgres).  

The database will keep track of uncompleted and completed jobs, flight information about Hermes, and information about the bussing system in East Lansing.  

##### Client-Side Script

This script will act as the glue between the API and Hermes and will be written in Python.  It will send and receive information to and from Hermes and the API by working with [Mission Planner](https://ardupilot.org/planner/).  This is because Hermes is unable to communicate directly with the API and implementing this to be on-board the drone is out of the scope of this project.  Keeping this communication separate from the drone has its pros and cons but will not be further discussed in this document.  

*Edit: 7 February 2023*
- The client-side script is now called [[Beacon]].
- Implementing the on-board communication is now in-scope of the project using Lua scripts.
  

# Diagrams

# ![](https://lh6.googleusercontent.com/gyVBW9nPgSGXS7ESM0HNLRVs2v7Sa0lYPWxg_N6aHuqZ2QnCI5SXU3SC6CW203lZVYLH1rDtiRbRAMHXSJbjo1whDqdulcxCDmt2_JIFZdEkJB8Hji3YPIyJnjqou9ATa5Vv40T3kfPbBbBh9QkRPWU)

# Future

##### Onboarding 

For this project, we are only focusing on communicating with Hermes and storing information about the buses in East Lansing.  However, it can be understood that if the project were to expand to include more drones or other cities, that information would need to be onboarded to Atlas.  An onboarding process would be a nice feature to have but is currently out-of-scope of the project.  If time permits and the current goals of the service are met, this is something that could be pursued next.
