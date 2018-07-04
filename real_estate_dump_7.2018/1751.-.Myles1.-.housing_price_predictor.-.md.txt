# Housing Price Predictor

# What it does
The Housing Price Predictor makes use of publically avaible real estate data in the Seattle area to train an XGBoost model. This allows for predictions of present and past values of real estate within a 10% absolute median error.

# Use Cases

1. Tracking price fluctuations over time.

2. A seller would like to make changes to their property before putting it on the market. They input their address, and receive value predictions. The seller then changes the input variables and receives updated predictions. This allows them to make changes to their property, knowing beforehand what kind of change in value they can expect.




# Technologies
1. Python
3. Amazon AWS (S3 & EC2)
4. Scikit-learn
5. Numpy
6. Pandas
7. Matplotlib


# Examples

Images created with Matplotlib

These first two images show the comparison between two properties with actual sales (blue points) and predicted value (red line)

![](/images/sales_and_prediced_values_1.png?raw=true)

![](/images/sales_and_prediced_values_2.png?raw=true)

These are the expected changes in price based on a few different options for remodeling.

![](/images/price_changes_1.png?raw=true)
