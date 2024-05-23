The project is divided into three sections:

Flask:
	• Flask will retrieve the created and closed issues, Pull Requests, Releases, Contributors, Branches, and Commits for the specified repository for the past two months. 
	• It will also retrieve the author_name and other details for the created and closed issues. 
	• Flask will obtain the repository_name from the body of the api (i.e. from React).
	• It will first use the data from GitHub and pass it as an input request in the POST body to LSTM microservice in order to forecast and predict the data. 
	• It will then use group_by to group the created and closed issues for a given month and return the data to client. 
	• The response obtained from LSTM microservice is also returned back to the client.

LSTM: 
	• Based on the previous 30 days, LSTM will forecast the data for the previous two months after receiving the GitHub data from the Flask microservice.
	• Additionally, it will use the matplot library to plot three distinct graphs. They are "model_loss," "lstm_generated_data," and "all_issues_data". 
	• It will use StatsModel 4 to generate graphs for forecasting and observations. It will produce trend, weekly, and daily graphs as well as forecasting components.
	• This graph will be kept in a gcloud storage bucket as an image. After that, the picture URL is sent back as a JSON response to the Flask microservice. 

React: 
	• React will obtain from GitHub all the requirements for a specified repository and show the same using high-charts as bar charts, line charts, and stack bars.        
	• Additionally, it will provide the predicted data images for the specified GitHub repository, with the images being received from GCP storage 
	• React will contact the Flask microservice through the fetch api.

Implementation: 
	• First, all 15 repositories' issues, pull requests, releases, contributors, branches, and commits were retrieved from Github.
	• Moreover, delivered the data in the form of a JSON body to the LSTM service, which is located on the GCP cloud or localhost on port 8080.
	• Using the collected data, LSTM creates all the necessary graphs and saves the information in Google Cloud Bucket storage. 
	• The links to the graph images are sent back to the Flask app by the LSTM service.
	• Following that, Flask sends the URL of each image as a JSON request to the React application running locally on port 3000 or on the GCP cloud. 
	• Recat gathers all of the links before populates the images.

Commands to run every microservice:
	To run locally on the system,
For Flask and LSTM:
	• python -m venv env
        • env\Scripts\activate.bat
        • pip install -r requirements.txt
        • python app.py  

For React:
	• npm install
	• npm start

	To run and deploy microservices on Google cloud,
	• Need to build docker image and then pushing the docker image into cloud clearly mentioned on readme files.

Successfully deployed all the microservices LSTM, Flask and React on the Google Cloud.



