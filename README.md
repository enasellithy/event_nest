## Installation

- node
- npm 
- docker (if running through Docker)

- git clone https://github.com/enasellithy/event_nest

## Docker Deployment

### Build and Run the Docker Container

1. Build the Docker image:
 
   ```bash
   docker build -t nestjs-app .

   ```bash
   docker run -p 3000:3000 --env-file .env nestjs-app

### Or Local Development Setup

- cd event_backend
- npm install --legacy-peer-deps
- cp env .env

```
    host: process.env.DB_HOST,
    port: 3306,
    username: 'root',
    password: process.env.DB_PASSWORD,
    database: 'event_ticketing',


### Database Setup

in SQL 
    ````
    CREATE TABLE `event` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `date` datetime NOT NULL,
  `ticketsAvailable` int(11) NOT NULL,
  `status` ENUM('Available','Sold Out') NOT NULL DEFAULT 'Available',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

    ````
    CREATE TABLE `event` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `date` datetime NOT NULL,
  `ticketsAvailable` int(11) NOT NULL,
  `status` ENUM('Available','Sold Out') NOT NULL DEFAULT 'Available',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

  ````````````` Insert Simple Data

  INSERT INTO `event`(`name`, `date`, `ticketsAvailable`) VALUES ('event 1','2025-3-25',100);
INSERT INTO `event`(`name`, `date`, `ticketsAvailable`) VALUES ('event 2','2025-3-25',75);
INSERT INTO `event`(`name`, `date`, `ticketsAvailable`) VALUES ('event 3','2025-3-25',20);


Create an Order:


mutation {
  purchaseTickets(orderNumber: "ORDER123", eventId: 1, ticketsPurchased: 2) {
    id
    orderNumber
    ticketsPurchased
    event {
      id
      name
      ticketsAvailable
    }
  }
}

Get All Events:

query {
  events {
    id
    name
    date
    ticketsAvailable
  }
}

Get a Single Event:


query {
  event(id: 1) {
    id
    name
    date
    ticketsAvailable
  }
}
