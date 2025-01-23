# Human Resources Mobile Application Android
Mobile apps for employees to access web application human resources and many features giving more easier access anywhere and anytime.

## Features
- User login that integrate with web app
- Geotagging and take picture for attendance 
- Perform leave request and approval
- Check payslip data

# Technologies
Build using .NET Maui, latest .NET frameworks features for mobile development. integrated with RESTful API for Database Communication and XAML for front end side create user interface and experiences.

![.NET MAUI](https://img.shields.io/badge/.NET%20MAUI-%235C2D91.svg?style=for-the-badge&logo=dotnet&logoColor=white)  ![RESTful API](https://img.shields.io/badge/RESTful%20API-%2300843e.svg?style=for-the-badge&logo=api&logoColor=white)  ![XAML](https://img.shields.io/badge/XAML-%230C54C2.svg?style=for-the-badge&logo=xml&logoColor=white)

### API Communication

* POST
```csharp
await AuthLogin.HttpPost(json, "api/Auth/Login"); // Login
```

* GET

Initiate from page.cs
```csharp
await AuthLogin.HttpGet("", "/api/wf/getAttendanceType"); // Get attendance type for taking attendance
```

### Save & Consume Login Data
  
* Write
```csharp
using (StreamWriter writer = File.CreateText(fileName))
{
    writer.WriteLine(writedata);
}
```

* Read
```csharp
using (StreamReader reader = File.OpenText(fileName))
{
  string line = reader.ReadLine();
  value = line;
}
```

### Geotagging
.NET Frameworks features geotagging location access user's phone current location and provide mock location security validation. Get location used for attendance menu for employees absence from current device location.
* Get Location (Latitude & Longitude)
```csharp

using Microsoft.Maui.Maps;
using Microsoft.Maui.Controls.Maps;

GeolocationRequest requests = new GeolocationRequest(GeolocationAccuracy.Medium, TimeSpan.FromSeconds(10));
_cancelTokenSource = new CancellationTokenSource();
Location location = await Geolocation.Default.GetLocationAsync(requests, _cancelTokenSource.Token);
laLatitude = location.Latitude.ToString();
Longitude = location.Longitude.ToString();
```
* Check Mock Location
```csharp
if (location.IsFromMockProvider){
  // phone is using mock location
}
```
* Calculate Distance Between Current and Office Location
```csharp
public double GetDistance(GeoCoordinate other)
{
    const double earthRadius = 6371; // Earth's radius in kilometers

    // Convert latitude and longitude from degrees to radians
    double lat1Rad = Math.PI * currentLatitude / 180;
    double lon1Rad = Math.PI * currentLongitude / 180;
    double lat2Rad = Math.PI * officeLatitude / 180;
    double lon2Rad = Math.PI * officeLongitude / 180;

    // Calculate differences between coordinates
    double deltaLat = lat2Rad - lat1Rad;
    double deltaLon = lon2Rad - lon1Rad;

    // Haversine formula
    double a = Math.Sin(deltaLat / 2) * Math.Sin(deltaLat / 2) +
               Math.Cos(lat1Rad) * Math.Cos(lat2Rad) *
               Math.Sin(deltaLon / 2) * Math.Sin(deltaLon / 2);
    double c = 2 * Math.Atan2(Math.Sqrt(a), Math.Sqrt(1 - a));
    double distanceKm = earthRadius * c;
    double distance = distanceKm * 1000;
    return distance;
}
```

### Capture Image
Attendance menu features capture image as additional information for attendance data
```csharp
using (var stream = await result.OpenReadAsync())
  {
      // Resize Image from device camera
      byte[] resizedImageBytes = ResizeAndCompressImage(stream, 800, 600); 

      // Display  image
      myImage.Source = ImageSource.FromStream(() => new MemoryStream(resizedImageBytes));
  }
```
### Download Payslip Data
Empoyees can access payslip data and open it using browser
```csharp
await Launcher.Default.OpenAsync(payslipdata);
```

# API Endpoints Documentation

This document provides an overview of the API endpoints, their methods, and functionality.

## Endpoints Table

| Method     | API Endpoint            | Description             | Pages      |
|------------|-------------------------|-------------------------|------------|
| **POST**    | `/api/Application/GetApplicationData?_paramKey={ActivationCode}`            | Activation code validation         | Landing Page  |
| **POST**   | `/api/Auth/Login`            | Username and password validation for login       | Login Page   |
| **GET**    | `//api/role/empdata/`         | Fetch the user's data     | All Page   |
| **GET**    | `/api/role/menus/{username}`       | Fetch list of menu on dashboard      | Dashboard Pages   |
| **GET**    | `/api/wf/getAttendanceType`       | Fetch list attendance type     | Attendance Page   |
| **POST** | `/api/wf/submitAttendanceNew`       | Submit attendance     | Attendance Page   |
| **GET**    | `/api/wf/getDistanceOffice`         | Fetch the location of user's office     | Attendance Page   |
| **POST**    | `/api/role/changepassword/{newpassword}`         | Submit new password for change password     | Change Password Page   |
| **GET**    | `/api/wf/getDurationAndRemainingByDateFromTo/`         | Fetch the duration of leave request     | Leave Page   |
| **GET**    | `/api/wf/absence_type`         | Fetch list of absence type     | Leave Page   |
| **GET**    | `/api/wf/getDelegate`         | Fetch user's delegation     | Leave Page   |
| **GET**    | `/api/wf/getValidasiBeforeSubmit`         | Validation for request leave     | Leave Page   |
| **POST**    | `/api/wf/requestWithAttachment`         | Submit leave request     | Leave Page   |

### Usage Instructions
- **GET Requests**: Used for retrieving data from the server. 
- **POST Requests**: Used for creating new resources, such as adding a new  product.


###  Target Frameworks

.NET Frameworks = net 8.0

Android = 34.0


# Gallery
<img src="https://github.com/user-attachments/assets/d6ebcc46-7df0-470c-bf3f-8700a2f624d7" alt="Capture9" width="150" style="border-radius: 20px;">
<img src="https://github.com/user-attachments/assets/944a2c24-4127-4535-af54-39871a64b177" alt="Capture8" width="150" style="border-radius: 20px;">
<img src="https://github.com/user-attachments/assets/aead2f70-228d-4ea5-92fe-fbe5efcdb594" alt="Capture7" width="150" style="border-radius: 20px;">
<img src="https://github.com/user-attachments/assets/6f142545-f1b9-4b1e-822b-bac707157880" alt="Capture5" width="150" style="border-radius: 20px;">
<img src="https://github.com/user-attachments/assets/025a1abf-d39d-4a2c-9e6a-9a23ae094f1b" alt="Capture4" width="150" style="border-radius: 20px;">

