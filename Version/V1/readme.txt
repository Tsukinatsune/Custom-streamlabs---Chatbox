Class Methods

 constructor(config = {}) 

Initializes a new instance of the  Getmessage  class.

Parameters:

 config  (Object, optional): A configuration object.

 messageInterval  (Number): The time in milliseconds between message fetch requests. Defaults to 5000ms (5 seconds).

Behavior: Sets up internal properties like  baseUrl ,  streamlabsBase ,  messageInterval , and initializes an empty array for  listeners  and sets  messageTimer  to  null .

 addListener(callback) 

Registers a callback function to be notified when messages are fetched.

Parameters:

 callback  (Function): The function to execute when new data is received.

Behavior: Adds the provided  callback  function to the internal  listeners  array if it is indeed a function.

 notifyListeners(response, payload) 

Calls all registered listener functions with the fetched data.

Parameters:

 response  (any): The data or error object received from the API.

 payload  (any): The data sent in the request.

Behavior: Iterates through the  listeners  array and executes each callback function, passing the  response  object. Includes basic error handling for individual listeners.

 async sendRequest(payload) 

Sends an asynchronous HTTP request to the configured  baseUrl .

Parameters:

 payload  (String): The data to be sent in the request body (e.g., 'message').

Behavior: Uses the Fetch API to send a PUT request. It handles the response, parses it as JSON, and notifies listeners of the outcome (success or failure). Logs errors to the console and returns the fetched data on success.

 startMessageFetch() 

Starts the interval timer that periodically calls  sendRequest .

Behavior: Clears any existing timer to prevent duplicates, then sets up a new interval timer that executes  sendRequest('message')  at the frequency defined by  messageInterval .

 setMessageInterval(newInterval) 

Updates the interval for message fetching and restarts the fetch process.

Parameters:

 newInterval  (Number): The new interval in milliseconds.

Behavior: If  newInterval  is a valid positive number, it updates the  messageInterval  property and calls  startMessageFetch()  to apply the change. Logs an error for invalid input.

 stop() 

Stops the periodic fetching of messages.

Behavior: Clears the interval timer associated with message fetching and resets  messageTimer  to  null .

 init() 

Initializes the message fetching process.

Behavior: This method is essentially an alias for  startMessageFetch() , responsible for beginning the polling.
