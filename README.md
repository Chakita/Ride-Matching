# Ride Matching System 

Project built as a part of the Cloud Computing Course at PES University. The problem statement was set by the Professors and Teaching Assistants of the course.


A microservice architecture where multiple components communicate with each other using RabbitMQ <br>
When a request is sent to book a ride, the system gets your location and tries to match you with riders near your location.<br>
This project consists of 3 microservices - an HTTP server that accepts your requests for a ride, a microservice that tries to calculate the best drivers for the user ( actual ride-matching logic is not implemented, we just simulate the time taken), and a microservice that inserts the data into a database. 

## Architecture

1. A RabbitMQ docker container is setup and the required ports are exposed to enable connections from other services. <br>
2. The producer has 3 components
  a.  HTTP server to listen to ride requests so it can distribute that to consumers. <br> 
  The request to this endpoint will be of type POST and takes in the following information - 
			1. pickup
			2. destination
			3. time - The time in seconds that the consumer microservice will sleep for when data is received.
			4. cost
			5. seats
		
  b. HTTP server to listen to connection requests from new consumers and keep track of it
  This will be listening to POST requests from new consumers that contains the consumer_id and store their IP address and name. The Name and IP address will just be stored as a map, in an array, where each map has name and IP as the keys, and the consumer_id and the request IP as the values
  
  c. A RabbitMQ client to create queues and send the data to consumers. The RabbitMQ client in the producer will register a single queue for all the ride-sharing consumer microservice and one for the database microservice, and will be responsible for sending out the data from the POST requests to consumers.
  
3. There are 2 consumers - Ride mapping Consumer and the database consumer
  a. The ride mapping consumer will sleep for the specified time (since matching logic is not implemented) <br>
  b. The databse consumer will read the data from RabbitMQ and store the details into the database
  
