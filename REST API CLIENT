import java.io.*;
import java.net.*;
import org.json.JSONObject;

public class WeatherAPIClient {

    // Method to fetch weather data from OpenWeatherMap API
    public static String getWeatherData(String city, String apiKey) {
        String urlString = "https://api.openweathermap.org/data/2.5/weather?q=" + city + "&appid=" + apiKey + "&units=metric";
        StringBuilder result = new StringBuilder();

        try {
            // Create a URL object
            URL url = new URL(urlString);
            // Open a connection to the URL
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setConnectTimeout(5000); // Timeout in milliseconds
            connection.setReadTimeout(5000);

            // Check if the response code is 200 (HTTP OK)
            if (connection.getResponseCode() == 200) {
                // Read the response
                BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String line;
                while ((line = reader.readLine()) != null) {
                    result.append(line); // Append each line of the response
                }
                reader.close();
            } else {
                // Handle error response code
                System.out.println("Error: Unable to fetch weather data.");
                return null;
            }
        } catch (IOException e) {
            System.err.println("Error during API call: " + e.getMessage());
            return null;
        }

        return result.toString();
    }

    // Method to parse the JSON response and display weather data
    public static void displayWeather(String jsonResponse) {
        if (jsonResponse != null) {
            // Parse the JSON response
            JSONObject jsonObject = new JSONObject(jsonResponse);

            // Extract specific data from the JSON response
            String cityName = jsonObject.getString("name");
            JSONObject main = jsonObject.getJSONObject("main");
            double temperature = main.getDouble("temp");
            double humidity = main.getDouble("humidity");
            JSONObject weather = jsonObject.getJSONArray("weather").getJSONObject(0);
            String description = weather.getString("description");

            // Display the parsed data
            System.out.println("Weather Data for " + cityName + ":");
            System.out.println("Temperature: " + temperature + "°C");
            System.out.println("Humidity: " + humidity + "%");
            System.out.println("Description: " + description);
        } else {
            System.out.println("No data available to display.");
        }
    }

    public static void main(String[] args) {
        String apiKey = "your_api_key_here";  // Replace with your OpenWeatherMap API key
        String city = "London";  // City name for which you want to get weather data

        // Step 1: Fetch weather data
        String jsonResponse = getWeatherData(city, apiKey);

        // Step 2: Parse and display the weather data
        displayWeather(jsonResponse);
    }
}
