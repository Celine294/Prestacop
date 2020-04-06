# The PrestaCop Analyser
This service is responsible for retrieving the data stored in DynamoDB and analysing this data using spark. The results of the analysis are stored in a file called **"result.txt"** 

## Running the Service using IntelliJ
To run the service, there are two configurable parameters to provide in the following order:
- **The AWS region**: Give a region in which your DynamoDB table can be found, e.g. "eu-central-1"
- **The DynamoDB table name**: This is the name of the DynamoDB table in which all drone messages are stored

Create a new run configuration for the **Analyser** class. Add the above options as program arguments.

## Running the Analysis on AWS
First, SSH into the analysis instance. Its IP has been displayed by terraform (you can find it back with `terraform output`).

Then, run the command `sbt "run eu-central-1 prestacop" >> ~/result.txt`.

Wait ~10mins, and then you can show the results by running the command `tail ~/results.txt`.