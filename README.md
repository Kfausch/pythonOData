# pythonOData
How to pull data from Microsoft NAV or Business Central using OData API's and Python

My goal with this repository is to show how pyhton can be used to interact with your ERP data in Microsoft NAV or Business Cenertal - though this information is valuable for most API's that return JSON data.

First, to get data you can import requests and from request import HTTPBasicAuth. This will allow you to use requests.get which can you pass your API url, username, and password.
import requests
from requests.auth import HTTPBasicAuth
response = requests.get(url, auth=HTTPBasicAuth(username, password)


The data returned with OData API's is a dictonary with a nested list with another nested dictonary. I recommend Importing json and formatting your data so you can better understand where the data is within.
#easy way to format json data - get data > indent > print
data = get_data_from_api(odata_api_url, api_username, api_password)
dataFormat = json.dumps(data, indent=4)
print(dataFormat)

Once you can see your data you can use simple print statements to step into each section
print(data['value'][0]['Document_No']

As you get more fimiliar with the dataset you can do more advanced calculation and use other libraries such as Pandas or MatPlotLib. Here is an example of how you can use Panadas DataFrames to aggregate data.
df = pd.DataFrame(data['value'])
sales_by_customer = df.groupby('Sell_to_Customer_No')['Amount'].sum()
print(sales_by_customer)
