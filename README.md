# Capstone-Project
Final Project Summary
Dynamic Pricing for Urban Parking Lots
Project Overview
This project implements a real-time dynamic pricing engine for urban parking lots. Utilizing a simulated data stream, the system continuously adjusts parking prices based on various factors such as occupancy, queue length, traffic conditions, special events, vehicle type, and competitor pricing. The core objective is to optimize parking lot utilization and revenue by adapting prices to real-time demand and market conditions.

The solution is built around a streaming data pipeline using Pathway, with pricing models implemented from scratch using Python (NumPy and Pandas), and real-time visualizations powered by Bokeh.

Tech Stack
Python: The primary programming language for data simulation, pricing models, and orchestration.

Pathway: A powerful Python framework for building real-time data streaming applications. It handles data ingestion, transformations, and continuous computations.

Pandas: Used for data manipulation and preparation.

NumPy: Utilized for numerical operations within the pricing models.

Bokeh: An interactive visualization library for creating real-time, streaming plots that display the dynamic pricing behavior.

Google Colab: The execution environment for the entire project, providing a convenient platform for running Python notebooks.

Project Architecture and Workflow
The project follows a streamlined architecture designed for real-time data processing and visualization:

graph TD
    A[Synthetic Data Generation: dataset.csv] --> B(Pathway Data Ingestion Stream);
    B -- Records (timestamp, occupancy, capacity, traffic, etc.) --> C{Pricing Models};
    C -- Model 1: Baseline Linear --> C1[Price Model 1];
    C -- Model 2: Demand-Based --> C2[Price Model 2];
    C -- Model 3: Competitive --> C3[Price Model 3];
    C1 --> D(Bokeh Visualization Update);
    C2 --> D;
    C3 --> D;
    D -- Real-time Plotting --> E[User Interface / HTML Export];


Detailed Workflow:
Data Simulation (dataset.csv):

A synthetic dataset (dataset.csv) is generated to mimic real-world urban parking lot data. This includes timestamp, parking_space_id, latitude, longitude, capacity, occupancy, queue_length, traffic_level, is_special_day, vehicle_type, and competitor_price.

This dataset serves as the source for the simulated real-time data stream.

Pathway Data Ingestion:

The dataset.csv is ingested into a Pathway input stream.

autocommit_duration_ms is set to a small value (e.g., 100ms) to simulate continuous, real-time data arrival.

Pricing Models (Pathway UDFs):

Three distinct pricing models are implemented as Pathway User-Defined Functions (UDFs), allowing them to operate on the streaming data:

Model 1 (Baseline Linear): A simple model that adjusts prices linearly based on the current occupancy rate.

Model 2 (Demand-Based): A more sophisticated model that calculates a 'demand value' based on a custom function incorporating occupancy, queue length, traffic, special days, and vehicle type. The price is then derived from this demand.

Model 3 (Competitive): Builds upon Model 2 by also considering a simulated competitor_price and adjusting prices to remain competitive, especially at high or low occupancy rates.

Pathway's select operations apply these UDFs to the incoming data stream, continuously computing the dynamic prices for each parking space.

Real-time Visualization (Bokeh):

Bokeh is used to create interactive line plots.

A ColumnDataSource is initialized to hold the streaming data for the plots.

The main_bokeh_app function simulates the Pathway stream by iterating through the pre-generated df_dataset grouped by timestamp.

For each timestep, the calculated prices (from the plain Python functions mirroring the UDF logic) and other relevant metrics are streamed to the Bokeh ColumnDataSource.

The plots are then saved to a standalone HTML file (dynamic_pricing_plots.html) after the simulation completes, ensuring all data is captured and viewable in any web browser.

How to Run the Project
Open in Google Colab: The entire project is designed to run seamlessly in a Google Colab notebook.

Run Cells Sequentially: Execute each cell in the notebook from top to bottom.

Cell 1: Installs necessary libraries (pathway, bokeh, numpy, pandas).

Cell 2: Generates the synthetic dataset.csv.

Cells 3-6: Set up the Pathway data ingestion and define the three pricing models.

Cell 7: Initializes the Bokeh plots and ColumnDataSource.

Cell 8: Starts the simulated real-time data processing and visualization. This cell will print messages indicating progress and will save the final plots to an HTML file.

View Plots:

After Cell 8 completes, a file named dynamic_pricing_plots.html will be generated in your Colab environment.

You can download this file from the left-hand sidebar (folder icon) in Colab and open it in any web browser to view the interactive plots.

Relevant Documentation
dataset.csv: The synthetic dataset used for simulation.

dynamic_pricing_plots.html: The generated HTML file containing the interactive Bokeh visualizations of the dynamic pricing models.

Repository Access
This repository is public, and all code is accessible for review.
