# Android MVVM Architecture
This is a project used to show how the Android App should be organized.

MVVM stands for Model-View-ViewModel, and it is an architecture pattern designed to 
make code clean, maintainable, and reusable. It is widely used in modern Android app 
development due to its separation of concerns and better integration with lifecycle-aware 
components.

# Components of MVVM

-> Model

  - Handles data and business logic.
  - Responsible for fetching data from APIs, databases, or other sources.
  - Contains the raw data structure (e.g., POJOs like Employee and EmployeeResponse).

Example:
A model might represent an API response or a database entity.

-> View

  -Represents the UI elements, such as Activity, Fragment, or XML layouts.
  -The View's job is only to display data to the user and pass user actions (e.g., button clicks) to the ViewModel.
  -The View does not process or manipulate data directly.

Example:
activity_main.xml for layout design and MainActivity.kt to connect UI with the ViewModel.

-> ViewModel

  -Acts as a bridge between the Model and the View.
  -It handles business logic and updates the View whenever there is a change in data.
  -Uses LiveData or StateFlow to expose data to the View.
  -Keeps UI data alive during configuration changes (like screen rotation).

Example:
EmployeeViewModel fetches employee data and exposes it to the View through LiveData.



MyApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/myapp/
│   │   │   │   ├── data/
│   │   │   │   │   ├── model/
│   │   │   │   │   │   └── Employee.kt
│   │   │   │   │   │   └── EmployeeResponse.kt
│   │   │   │   │   ├── repository/
│   │   │   │   │   │   └── EmployeeRepository.kt
│   │   │   │   ├── network/
│   │   │   │   │   └── ApiService.kt
│   │   │   │   │   └── RetrofitClient.kt
│   │   │   │   ├── ui/
│   │   │   │   │   ├── adapter/
│   │   │   │   │   │   └── EmployeeAdapter.kt
│   │   │   │   │   ├── view/
│   │   │   │   │   │   └── MainActivity.kt
│   │   │   │   │   ├── viewmodel/
│   │   │   │   │   │   └── EmployeeViewModel.kt
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml
│   │   │   │   │   ├── item_employee.xml
│   │   │   └── AndroidManifest.xml
│   ├── build.gradle


# Explanation of Structure

1. data/

Contains the models (Employee.kt, EmployeeResponse.kt) to represent the API data.
Repository (EmployeeRepository.kt) acts as the data source, communicating with the API and preparing data for the ViewModel.

2. network/

Contains the API-related code:
ApiService.kt: Retrofit interface for defining API endpoints.
RetrofitClient.kt: Singleton class for initializing Retrofit.

3. ui/

adapter/: Holds the RecyclerView adapter (EmployeeAdapter.kt) for displaying the list of employees.

view/: Contains UI components like MainActivity.kt.

viewmodel/: Contains EmployeeViewModel.kt, which manages UI-related data and handles the business logic.

4. res/layout/

Contains layout files for activities and list items:

activity_main.xml: Layout for the main activity with RecyclerView.
item_employee.xml: Layout for individual employee list items.

5. AndroidManifest.xml

Defines the application metadata, activities, permissions, etc.

6. build.gradle

Contains project dependencies and configuration for building the app.

# Summary:

Model: API se data fetch karta hai (Employee, EmployeeResponse).

ViewModel: Logic handle karta hai aur View ko update karta hai (EmployeeViewModel).

View: Sirf data ko dikhata hai (MainActivity, activity_main.xml).

Repository: Model aur ViewModel ke beech ka mediator hai (EmployeeRepository).

Adapter: RecyclerView ko data bind karta hai (EmployeeAdapter).