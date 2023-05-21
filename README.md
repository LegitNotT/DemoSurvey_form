# DemoSurvey_form
This is the HTML code for a very basic Survey form
<!DOCTYPE html>
<html>
<head>
  <title>Demo Survey Form</title>
</head>
<body>
  <h1>Demo Survey Form</h1>
  
  <form action="/submit-survey" method="post">
    <h2>Personal Information</h2>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required><br><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required><br><br>

    <label for="dob">Date of Birth:</label>
    <input type="date" id="dob" name="dob" required><br><br>

    <h2>Checkbox Questions</h2>
    <label for="interests">Interests:</label><br>
    <input type="checkbox" id="interest1" name="interests" value="sports">
    <label for="interest1">Sports</label><br>
    <input type="checkbox" id="interest2" name="interests" value="music">
    <label for="interest2">Music</label><br>
    <input type="checkbox" id="interest3" name="interests" value="art">
    <label for="interest3">Art</label><br><br>

    <h2>Radio Questions</h2>
    <label for="gender">Gender:</label><br>
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">Male</label><br>
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">Female</label><br>
    <input type="radio" id="other" name="gender" value="other">
    <label for="other">Other</label><br><br>

    <h2>Dropdown Questions</h2>
    <label for="country">Country:</label>
    <select id="country" name="country">
      <option value="ind">India</option>
      <option value="canada">Canada</option>
      <option value="uk">UK</option>
      <option value="usa">USA</option>
    </select><br><br>

    <input type="submit" value="Submit">
  </form>
  <?php
	//to check if the email id exists
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $email = $_POST["email"];

    $emailExists = false;

    if (!$emailExists) {
      <script>document.getElementById('email-error').textContent = 'Email ID does not exist.';</script>;
    }
  }
  ?>
  <?php
	//to check if the user is greater than 18 or not
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $email = $_POST["email"];
    $dob = $_POST["dob"];

    //calculateing age
    $currentDate = new DateTime();
    $birthDate = new DateTime($dob);
    $age = $currentDate->diff($birthDate)->y;

    if ($age < 18) {
      <script>document.getElementById('age-error').textContent = 'You are a minor.';</script>;
    }
  }
  ?>
    <?php
	//to check if the user's country matches the selected country
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
      
      $selectedCountry = $_POST["country"];

      //to get IP
      $userIP = $_SERVER["REMOTE_ADDR"];

      // Some coding help from ChatGPT
      $geolocationURL = "https://api.ipgeolocation.io/ipgeo?apiKey=YOUR_API_KEY&ip=$userIP";
      $response = file_get_contents($geolocationURL);
      $data = json_decode($response);

      if ($data->country_code2 !== $selectedCountry) {
        <script>alert('Please select your current country.'); history.go(-1);</script>;
        exit; // Stop further execution
      }

      $name = $_POST["name"];
      $email = $_POST["email"];
      $dob = $_POST["dob"];
    }
  ?>
</body>
</html>
