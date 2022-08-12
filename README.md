# Ride Matching System 
A microservice architecture where multiple components communicate with each other using RabbitMQ <br>
When a request is sent to book a ride, the system gets your location and tries to match you with riders near your location.<br>
This project consists of 3 microservices - an HTTP server that accepts your requests for a ride, a microservice that tries to calculate the best drivers for the user ( actual ride-matching logic is not implemented, we just simulate the time taken), and a microservice that inserts the data into a database.

