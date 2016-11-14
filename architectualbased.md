# Architectual based contract by Viking
## Introduction 
This contract is an assignment written for contract based development, with the main focus on the requirement based subcontracting. The subcontract is based on a car rental company case, which need to get a online booking system developed. The company, named “Faraday” wish to have a web service meant for third party solutions, and through a desktop application meant for employees in the travel agencies.

This contract is created by team Viking. 

## Vision
_General description of the systems_  
The system should be available as a desktop application for travel agencies, and as a service for the third parties, and it should enable system users (employees and customers) book a rental car, see/cancel the booking.  

_General description of the purpose of the system_  
The system will digitalize the booking process and the system users(customers and employees) can book a car and see/cancel their booking online instead of calling/visiting Faraday.

## Constraints

* Airports are identified by their three letter IATA airport code  
* Hotels are identified by a 6 digit number  
* Rental	cars are identified by their licence plate  
* Licence plate numbers are max ten alphanumeric characters  
* The type of cars will be specified by the alphabet from A to F. The alphabet specifies the price and number of seats  
* The driver should be at  least 25 years old  
* If the place for pickup and delivery are not same, extra fee will be charged  
* The place for pickup and delivery should be the same city  
* Booking period is max 3 weeks  

## Use Case Model
![Domain model](/images/UseCaseDiagram.PNG)

* See list of rental cars  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Show a list of available cars for rent - including car type in a city in a given time period  
* Make booking
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a booking for up to 3 weeks of a specific car, either with the same pickup and delivery place or with two different places. Error if the car is no longer available.  
* See booking
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;See a booking, given the drivers licens number from the booking  
* Cancel booking
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cancel a booking, given the drivers license number from the booking

##Actors
* Customer  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The customer is the primary user for the car rental webservice.  

* Employee  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The employee is the primary user for the desktop application.  

##Domain Model

![Domain model](/images/DomainModel_Faraday.png)

* A customer or or travel agency will book one of the Faraday’s rental cars.
* A driver will pick up/deliver a booked rental car at a pickup station which is either a hotel or an airport
* Pick up and deliver station can be different.
* A driver will be identified by driver’s license number and name as in his/her passport.
* A rental car has a type that specify a price and number of seat.

##Non-functional requirement for the system
Seeing as the system will handle a great deal of personal information, the integrity of that customer information should be paramount.
* Webservice should be running HTTPS for added security measures.
* Customer information should be hashed and salted, as we are dealing with sensitive information IE Drivers License Numbers. 
* The webservice for third party solutions should be intuitive, and show the correct fleet of vehicles only at the pickup destination the customer chose. 
* Response time for the webservice must be able to process a booking within 5 minutes.
* All customer information, either obtained from the webservice or the desktop application, should be normalized as much as possible.
* Database design must follow a logical structure, making it easy to see which vehicles are available at which location. 
* If a booking is started but not completed, customer data should be removed from the database after 30 days. 
* Customer data for completed bookings are saved for eternity.
* Database must have multiple backup sources, as ensuring data integrity is of utmost importance

##Fully dressed use case description for ONE use case
**Use case name**: Booking through webservice  
**Primary actor**: Customer  
**Goal**: Customer makes successful rental car booking　　
**Stakeholder interests**:
* Customer - Wants to reserve a car, at a specific location and a specific time
* Rental company - Wants to ensure as many vehicles as possible gets rented out

**Preconditions**: The customer MUST have a valid driver's license  
**Minimal guarantees**: Error message: Booking failed  
**Success guarantees**: Success message: Booking complete  
**Main success scenario**:   
1.1 The customer visits the rental company's website.  
1.2 The customer picks a location from where he/she wants to rent a car.  
1.3 The customer picks a date and time period for the rental.  
1.4 The customer is shown a selection of vehicles available for rental at the chosen location.  
1.5 The customer picks which model of vehicle to be rented EI model A to F.  
1.6 The customer submits the relevant rental information (Driver's license number, Identifying information).  
1.7 The information is processed to ensure the drivers license is valid.  
1.8 The customer now picks payment options, either pay directly through the website (Credit card or bank transfer) or direct payment at rental company.  
1.9 Additional options such as insurance is chosen or left alone.  
2.0 Booking is being processed and payment charged (In case of payment through website).  
2.1 Booking is completed and receipt shown to customer.  

## Definition of non-functional requirements 
A non-functional requirement is something that decides how the program should behave, rather than a specific functionality. Non-functional requirements can best be explained as “quality attributes” so an example could be a non-functional requirement that says the system should run at a certain speed, or it should take no longer than X to complete an action. Non-functional requirements can also be said to be the “ilities” for example Accessibility, Portability, Reliability are non-functional requirements.  

##Prioritize these architectural drivers (Non-functional requirements) 
The non-functional requirements have been prioritized for data integrity and protection. Faraday’s customer information should be held at high regard, as loss or leaking of said information would reduce the trust in Faraday’s brand.  

* Customer data for completed bookings are saved for eternity.  

* Database must have multiple backup sources, as ensuring data integrity is of utmost importance  

* Website should be running HTTPS for added security measures.  

* Database design must follow a logical structure, making it easy to see which vehicles are available at which location.  

* The website for third party solutions should be intuitive, and show the correct fleet of vehicles only at the pickup destination the customer chose.  

* Response time for the website must be able to process a booking within 5 minutes.  

* If a booking is started but not completed, customer data should be removed from the database after 30 days. 

## System architecture
### Package/component diagram with dependencies
![Component/package diagram](/images/ComponentPackageDiagram.PNG)

### Specification of services of each of the packages
#### Components
_Application component_ provides service that can be used by system user.  
_Booking component_ provides logic for booking to the applications.  
_Data access component_ provides provides data to Booking package.  

#### Packages
_UI_ provides visual presentation to the system user.  
_Form_ handle the inputs from the system user.  
_Check Cars_ provides information of available cars.  
_See booking_ provides information of the booking that has been made earlier.  
_Make booking_ handle booking of a rental car.  
_Cancel booking_ handle cancelling of the booking that has been made earlier.  

#### Define the principal of interaction between the packages
_UI_ will have a _Form_ which the system user can insert data for _Check cars_/_See booking_/_Cancel booking_/_Make booking_.  

_Check cars_/_See booking_/_Cancel booking_/_Make booking_ gets data from _Data access_ component and send the information/message back to _UI_  

#### Show it in a architectural interaction diagram
![Architectual interaction diagram](/images/ArchitecturalInteractionDiagram.png)
*1) makeBooking(startDate,endDate,startTime,endTime,pickUpStation,deliveryStation,typeOfCar,driverslicenseNumber,driverName)  

## Show an implementation of the architecture for one scenario (Technical proof of concept for the architecture) 
This is a VERY simplified proof of concept architecture of MakeBooking.  

![Packages](/images/Packages.PNG)

The UI is represented by a simple console, which has an instance of the BookingFacade - The main idea is the UI represent the desktop application / Third party application. This way, the UI can call all the given methods for the bookings. In this case makeBooking which is the only method implemented. 
The booking takes the arguments:  
makeBooking(startDate,endDate, startTime,endTime,pickUpStation,deliveryStation, typeOfCar,driverslicenseNumber,driverName)  
![Facade](/images/Facade.PNG)

The booking facade have an instance of the controller, which contains the method. 
![BookingFacade](/images/BookingFacade.PNG)

The controller class creates a booking object, and send it to the DBfacade, which takes an object  serialize (Normally you have a real database, but this one just serialize it and saves it)
![Controller](/images/Controller.PNG)

The DBfacade calls the method saveBooking in our “Database”. In this case we just save the booking object in “booking.ser”. No real thing is implemented  
![Database](/images/Database.PNG)
If everything went well in the process the UI will get the “success” message - otherwise “fail”.  

## The persistency of the system
### ER-model 
![ERmodel](/images/ER-Model.png)

## Justification of you decisions
As this project is a very simplified case, we wanted to keep it as simple as possible. Because there is both third party applications and a desktop program - it was obvious to create a facade which can be implemented in any application and call our booking system. The facade should be compared to an API or a web service. This is an simple and easy solution. 

## Requirements
### Brief presentation of the system
Shown below is a representation of the logical database structure.
![Logical data model](/images/LogicalDataModel.png)
## Design specification document
### Class diagram
![Class diagram](/images/ClassDiagram.png)
![Class diagram](/images/ControllerDiagram.png)
## Sequence diagrams for "checkCars" and "makeBooking"
![Sequence diagram](/images/SequenceDiagram.png)
You may assume that all driver’s licence numbers are valid, as we have not found any service API for driver’s licence validation yet.
### State diagram
![State diagram](/images/StateDiagram.png)
### Relational model
![Relational model](/images/RelationModel.png)
