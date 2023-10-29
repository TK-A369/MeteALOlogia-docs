REST API
========

In our project, database's REST API will be used primarily in two ways:

Sending measurements to database by the station
-----------------------------------------------

Weather station will periodically send measurements to the database server.

Those data aren't secret, so it isn't necessary to encrypt them.
However, they should be signed, so server knows that authentic station sent them.
If we didn't use signing, then a malicious person could send false data to server.
This could, for example, easily lead to overfilling server's memory.

Another solutions could be to accept data only from given IP. Or use encrypted protocol (i.e. HTTPS) and transmit API key every time.

We decided to use DSA algorithm to sign messages sent by the station. Then, database will verify them.

When setting station up, we will generate a keypair.
Private (signing) key will be saved in station.
Public (verifying) key will be saved in database.

Receiving measurements by the clients
-------------------------------------

Clients - both website server, and potentially other devices - will use this API to access weather data.

Using API to get data doesn't require any kind of authentication nor signing.
