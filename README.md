# MLOps-challenge

This project was designed as a techincal challenge for data science team appreciation. It is based on the Hotel Booking Prediction Kaggle notebook, which uses data available [in this link](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand?resource=download), as part of the [Hotel Booking Demand Datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191), and aims to classify if, given a booking data information, it will be canceled (1) or not(0).
The model used was the CatBoost, trained based on the project's description notebook, available [here](https://www.kaggle.com/code/niteshyadav3103/hotel-booking-prediction-99-5-acc). The model was choosen by accuracy score evaluation available in the end of the notebook.

# Installation
## Prerequisites
* Docker and docker-compose;

## Installation steps
* Clone the repository;
* Create a folder named model on project's root folder;
* Download the .csv dataset [here](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand?resource=download) and paste it inside model folder;
* Run `docker-compose up -d` to run the containers.

# Usage

## Tests
To run the available tests, you can use `docker exec -it mlops-challenge-app-1 pytest`

## MLFlow
Mlflow application for model metrics overview is available at `http://localhost:5000`. For proper working, model training needs to be done before acessing MLFlow, by the available route given below.

## API
This project was based on Flask API, with tree main routes to use. The API is available locally by the link `http://localhost:8000`.

## Routes

### ´/´
* Method: GET;
* Inputs: None;
* Outputs: Text "MLOps Technical Challenge API"

### ´/model/fit´
* Method: GET;
* Inputs: None;
* Outputs: Text "Model trained successfully!";
* Description: Model training route. When succeeded, it will make metrics available in the MLFlow application.

### ´/model/predict´
* Method: GET;
* Inputs: JSON with dataset columns as keys and values as described in the article;
* Outputs: JSON with prediction class;
* Description: Model prediction route. If no model was trained first, it returns an 400 error code.

Input example:
```
{
	"reservation_status_date": "10/27/2017",
	"hotel": "Resort Hotel",
	"meal": "SC",
	"market_segment": "Direct",
	"distribution_channel": "Direct",
	"reserved_room_type": "E",
	"deposit_type": "Refundable",
	"customer_type": "Transient",
	"lead_time": 457,
	"arrival_date_week_number": 43,
	"arrival_date_day_of_month": 10,
	"stays_in_weekend_nights": 2,
	"stays_in_week_nights": 2,
	"adults": 2,
	"children": 0,
	"babies": 0,
	"is_repeated_guest": 0,
	"previous_cancellations": 0,
	"previous_bookings_not_canceled": 1,
	"required_car_parking_spaces": 0,
	"total_of_special_requests": 0,
	"agent": 8,
	"company": 110,
	"adr": 120,
	"days_in_waiting_list": 0,
	"arrival_date_year": 2015,
	"assigned_room_type": "C",
	"booking_changes": 3,
	"reservation_status": "Check-Out",
	"country": "PRT",
	"arrival_date_month": "October",
	"is_canceled": 0
}
```

Output example:
```
{
	"pred_class": 1
}
```
