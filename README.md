Driver App Features
1. Launch Options (Register & Login)
•	Use Activity or Fragment for Register and Login screens.
•	Implement the following fields for registration:
o	First Name, Last Name, Phone Number, 4-digit Pin (Password), Gender, Email, County, Sub-county.
o	Use a Spinner for dropdowns (County/Sub-county).
o	Fetch dropdown data using an API and populate sub-county dropdown dynamically based on the selected county.
Validation:
•	Ensure non-empty fields, valid phone numbers, and email format.
•	Use Retrofit for API communication to validate data.
________________________________________
2. Persistent Login
•	Save login state using SharedPreferences.
•	Check login state in onCreate() of the main activity:
kotlin
CopyEdit
val sharedPreferences = getSharedPreferences("DriverApp", Context.MODE_PRIVATE)
val isLoggedIn = sharedPreferences.getBoolean("isLoggedIn", false)
if (isLoggedIn) {
    startActivity(Intent(this, HomeActivity::class.java))
    finish()
}
________________________________________
3. Navigation Drawer
Use a NavigationView with:
•	Home: Displays a map with a "Go Online/Go Offline" toggle button. Use Google Maps SDK.
•	Profile: Displays driver details fetched from the backend.
•	My Rides: Lists ride requests for the driver with their status.
Go Online/Offline:
•	Change the driver's status via an API call and toggle button text.
________________________________________
4. Notifications for Ride Requests
•	Use Firebase Cloud Messaging (FCM) for push notifications.
•	When a ride request is received:
o	Show a map and customer details (name, phone, pick-up, drop-off, passengers).
o	Add Accept and Decline buttons.
o	Use Retrofit to notify the backend about the driver's response.
________________________________________
Customer App Features
1. Launch Options (Register & Login)
Similar to the Driver App:
•	Registration includes First Name, Last Name, Phone Number, 4-digit Pin (Password), Gender, Email, County, Sub-county.
•	Fetch counties and sub-counties from the backend.
Persistent Login:
•	Use SharedPreferences to retain login state.
________________________________________
2. Navigation Drawer
Use a NavigationView with:
•	Home: Displays a map with a "Request Ride" button.
•	Profile: Displays customer details fetched from the backend.
•	My Rides: Lists ride history fetched via an API.
________________________________________
3. Request Ride Flow
•	On clicking "Request Ride," show a form with:
o	Pick-up Point, Drop-off Point, Number of Passengers.
•	Validate and send the request to the backend.
•	Show appropriate messages based on driver availability:
o	Offline: Inform the customer.
o	Online: Notify the driver.
________________________________________
4. Notification for Driver's Response
•	Use FCM to receive updates on ride status:
o	Declined: Inform the customer.
o	Accepted: Show driver details (name, phone, gender, email, county, sub-county).
Customer's Response:
•	Accept: Notify the backend and update the driver.
•	Decline: Notify the backend and return to the home screen.
________________________________________
Backend Integration
1.	Authentication API
o	Endpoint for login, registration, and status updates.
2.	County/Sub-county API
o	Endpoint to fetch counties and sub-counties.
3.	Ride Request API
o	Endpoint to create ride requests, fetch ride status, and notify drivers.
4.	Notification API
o	Endpoint to send notifications for ride requests and responses.
________________________________________
Technologies & Tools
•	Frontend (Android Apps):
o	Language: Kotlin/Java
o	Libraries: Retrofit, Glide, Google Maps SDK, Firebase (FCM), Jetpack Navigation
o	Storage: SharedPreferences, SQLite (for local caching if needed)
•	Backend API:
o	Framework: Laravel
o	Database: MySQL
o	Tools: Laravel Passport/Sanctum for authentication, FCM for notifications
•	Deployment:
o	Use Google Play Store for app distribution.
