
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

public class CurrencyConverter {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter the base currency (e.g., USD): ");
        String baseCurrency = scanner.nextLine().toUpperCase();

        System.out.println("Enter the target currency (e.g., EUR): ");
        String targetCurrency = scanner.nextLine().toUpperCase();

        System.out.println("Enter the amount to convert: ");
        double amount = scanner.nextDouble();

        try {
            double conversionRate = fetchExchangeRate(baseCurrency, targetCurrency);
            double convertedAmount = amount * conversionRate;

            System.out.printf("%.2f %s is equal to %.2f %s\n", amount, baseCurrency, convertedAmount, targetCurrency);
        } catch (IOException e) {
            System.out.println("Error fetching exchange rates: " + e.getMessage());
        } finally {
            scanner.close();
        }
    }

    private static double fetchExchangeRate(String baseCurrency, String targetCurrency) throws IOException {
        String apiKey = "YOUR_API_KEY"; // Replace with your API key
        String apiUrl = "https://api.example.com/exchange_rates?base=" + baseCurrency + "&symbols=" + targetCurrency;

        URL url = new URL(apiUrl);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");

        BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        StringBuilder response = new StringBuilder();
        String line;

        while ((line = reader.readLine()) != null) {
            response.append(line);
        }

        reader.close();
        connection.disconnect();

        // Parse the response to get the exchange rate
        // This part will depend on the structure of the API response
        // Assume the response is in JSON format with a key "rate" for the exchange rate
        double exchangeRate = parseExchangeRateFromApiResponse(response.toString());

        return exchangeRate;
    }

    private static double parseExchangeRateFromApiResponse(String response) {
        // Parse the response JSON to extract the exchange rate
        // This is a placeholder method assuming a certain structure in the API response
        // Replace this with your actual parsing logic based on the API response format
        return 1.12; // Placeholder value, replace with the parsed exchange rate
    }
}
